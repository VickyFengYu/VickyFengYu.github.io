Session vs JWT Based Authentication
===================


## <i class="icon-folder-open"></i> Session Based Authentication

A session variable's content is stored on the server, however, the session is identified by a session ID which is stored at the client and sent with each request. Usually the session ID is stored in a cookie, but it can also be appended to URL's.


![enter image description here](https://github.com/VickyFengYu/vickyfengyu.github.io/blob/master/image/springboot/session-auth-flow.png?raw=true)


## <i class="icon-folder-open"></i> JWT Based Authentication

Many web applications use JSON Web Token (JWT) instead of sessions for authentication. In the token based application, the server creates JWT with a secret and sends the JWT to the client. The client stores the JWT (usually in local storage) and includes JWT in the header with every request. The server would then validate the JWT with every request from the client and sends response.


![enter image description here](https://github.com/VickyFengYu/vickyfengyu.github.io/blob/master/image/springboot/jwt-auth-flow.png?raw=true)


## <i class="icon-folder-open"></i> Scalability

Session based authentication: Because the sessions are stored in the server’s memory, scaling becomes an issue when there is a huge number of users using the system at once.

Token based authentication: There is no issue with scaling because token is stored on the client side.



## <i class="icon-folder-open"></i> Multiple Device

Session based authentication: Cookies normally work on a single domain or subdomains and they are normally disabled by browser if they work cross-domain (3rd party cookies). It poses issues when APIs are served from a different domain to mobile and web devices.

Token based authentication: There is no issue with cookies as the JWT is included in the request header.

Token Based Authentication using JWT is the more recommended method in modern web apps. One drawback with JWT is that the size of JWT is much bigger comparing with the session id stored in cookie because JWT contains more user information.



## <i class="icon-folder-open"></i> Refresh Token Flow

Below are the steps to do revoke your JWT access token:

1) When you do login, send 2 tokens (Access token, Refresh token) in response to client .
2) Access token will have less expiry time and Refresh will have long expiry time .
3) Client (Front end) will store refresh token in his local storage and access token in cookies.
4) Client will use access token for calling apis. But when it expires, pick the refresh token from <mark>local storage </mark> and call auth server api to get the new token.
5) Your auth server will have an api exposed which will accept refresh token and checks for its validity and return a new access token.
6) Once refresh token is expired, User will be logged out.


```
//AngularJS

const storage = $window.localStorage;

```
