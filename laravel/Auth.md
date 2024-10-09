```

<?php

namespace App\Http\Controllers\Api;

use App\Http\Controllers\Controller;
use App\Http\Resources\UserResource;
use App\Models\RefreshToken;
use App\Models\User;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Facades\Validator;
use Illuminate\Support\Str;
use Symfony\Component\HttpFoundation\Response;

class AuthController extends Controller
{
    public function register(Request $request)
    {
        // Validate incoming request data
        $validator = Validator::make($request->all(), [
            'name' => 'required|string|max:255',
            'mobile' => 'required|string|unique:users',
            'password' => 'required|string|min:8',
            'email' => 'required|email|unique:users',
        ]);
    
        // Return validation errors if any
        if ($validator->fails()) {
            return response()->json([
                'status' => 'error',
                'message' => $validator->errors(),
                'data' => [],
            ], Response::HTTP_UNPROCESSABLE_ENTITY);
        }
    
        // Create the user
        $user = User::create([
            'name' => $request->name,
            'email' => $request->email,
            'mobile' => $request->mobile,
            'role' => 'user',
            'password' => Hash::make($request->password),
        ]);
    
        // Generate access token
        $accessToken = $user->createToken('access_token')->plainTextToken;
    
        // Check if the user was created successfully
        return response()->json([
            'status' => 'success',
            'message' => 'Account created successfully',
            'data' => [
                'user' => new UserResource($user),
                'token' => $accessToken,
            ],
        ], Response::HTTP_CREATED); 
    }
    public function login(Request $request)
    {
        // Validate the incoming request
        $validator = Validator::make($request->all(), [
            'mobile' => 'required|exists:users,mobile',
            'password' => 'required',
        ]);
    
        // Handle validation failure
        if ($validator->fails()) {
            return response()->json([
                'status' => 'error',
                'message' => $validator->errors(),
                'data' => [],
            ], Response::HTTP_UNPROCESSABLE_ENTITY);
        }
    
        // Retrieve the user by mobile number
        $user = User::where('mobile', $request->mobile)->first();
    
        // Check if the user exists and the password matches
        if (!$user || !Hash::check($request->password, $user->password)) {
            return response()->json([
                'status' => 'error',
                'message' => 'Mobile number or password is incorrect',   
                'data' => [],
            ], Response::HTTP_UNAUTHORIZED);
        }
    
        // If password matches, create the access token
        $accessToken = $user->createToken('access_token')->plainTextToken;
    
        // Generate refresh token
        $refreshToken = Str::random(64);
    
        // Save refresh token in the database
        RefreshToken::create([
            'user_id' => $user->id,
            'token' => hash('sha256', $refreshToken),   
            'expires_at' => now()->addDays(30),  
        ]);
    
        // Return the response with user, access token, and refresh token
        return response()->json([
            'status' => 'success',
            'message' => 'Login successful',
            'data' => [
                'user' => new UserResource($user),  
                'token' => $accessToken,
                'refresh_token' => $refreshToken,
            ],
        ], Response::HTTP_OK);
    }
    

  
    
    public function refreshToken(Request $request){
        $request->validate([
           'refresh_token' => 'required',
       ]);

        $hashedToken = hash('sha256', $request->refresh_token);

        $refreshToken = RefreshToken::where('token', $hashedToken)->first();

        if (!$refreshToken) {
           return response()->json([
               'status' => 'error',
               'message' => 'invalid refresh token',
               'data' => [],
           ], Response::HTTP_UNAUTHORIZED);
       }

       // Check if the refresh token has expired
       if ($refreshToken->expires_at < now()) {
            $refreshToken->delete();
           
           return response()->json([
               'status' => 'error',
               'message' => 'refresh token expired',
               'data' => [],
           ], Response::HTTP_UNAUTHORIZED);
       }

        $user = $refreshToken->user;

        $newAccessToken = $user->createToken('user_token')->plainTextToken;

        $newRefreshToken = Str::random(64);  

        $refreshToken->update([
           'token' => hash('sha256', $newRefreshToken),
           'expires_at' => now()->addDays(30), 
       ]);

       return response()->json([
           'status' => 'success',
           'message' => 'token refreshed',
           'data' => [
               'token' => $newAccessToken,
               'refresh_token' => $newRefreshToken,  
           ],
       ], Response::HTTP_OK);
   }
}
```
