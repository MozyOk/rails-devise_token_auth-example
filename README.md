# rails devise token auth example  

# SETUP

`bundle install`  
`rails db:create`  
`rails db:migrate`  
`rails s`  

If it doesn't work, try changing config/database.yml.

# HOW TO WORKS
## SignUp
`curl localhost:3000/api/auth -X POST -d '{"email":"example@example.com", "password":"password", "password_confirmation": "password"}' -H "content-type:application/json"`  

response
```
{"status":"success","data":{"id":1,"provider":"email","uid":"example@example.com","allow_password_change":false,"name":null,"nickname":null,"image":null,"email":"example@example.com","created_at":"2020-01-30T17:35:50.000Z","updated_at":"2020-01-30T17:35:51.000Z"}}% 
```  

## SignIn
`curl localhost:3000/api/auth/sign_in -X POST -d '{"email":"example@example.com", "password":"password"}' -H "content-type:application/json" -i`  

response
```
HTTP/1.1 200 OK
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Permitted-Cross-Domain-Policies: none
Referrer-Policy: strict-origin-when-cross-origin
Content-Type: application/json; charset=utf-8
access-token: 3YO-vj907oVgouq6fRqGHA
token-type: Bearer
client: nlhhfvXZtJ10y7VbgbNF4w
expiry: 1581615702
uid: example@example.com
ETag: W/"0b844d681927a23677ff78329b4c7409"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: 36fdb84a-2429-457b-819d-9c9ed766f78d
X-Runtime: 0.350010
Transfer-Encoding: chunked

{"data":{"id":1,"email":"example@example.com","provider":"email","uid":"example@example.com","allow_password_change":false,"name":null,"nickname":null,"image":null}}% 
```

## Change Password
※ **You need to change access-token, client and uid**  
`curl localhost:3000/api/auth/password -X PUT -d '{"password":"password_new", "password_confirmation": "password_new"}' -H "content-type:application/json" -H "access-token: 3YO-vj907oVgouq6fRqGHA" -H "client: nlhhfvXZtJ10y7VbgbNF4w" -H "uid: example@example.com"`  

response
```
{"success":true,"data":{"provider":"email","allow_password_change":false,"id":1,"email":"example@example.com","uid":"example@example.com","name":null,"nickname":null,"image":null,"created_at":"2020-01-30T17:35:50.000Z","updated_at":"2020-01-30T17:47:31.000Z"},"message":"Your password has been successfully updated."}% 
```

