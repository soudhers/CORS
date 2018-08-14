<pre>
1. CORS is between Browser and Server.
2. Client initiates HTTP request(from x.com domain) to back-end server(y.com). This fails SOP, so browser follows CORS.
3. Browser sends PREFLIGHT req to Server (which is HTTP OPTIONS method) with ACCESS_CONTROL_REQUEST_METHOD header set
4. Server responds with all the headers ACCESS_CONTROL_ALLOW_XXXX set.
      (XXXX is --->  METHODS(GET,POST...), HEADERS, ORIGIN(hostnames or *) (and CREDENTIALS if cookies are enabled))
5. Browser checks if the client domain is part of ACCESS_CONTROL_ALLOWED_ORIGIN. If yes, Browser sends the actual HTTP request to the server.
6. Server responds back with the result of Client's HTTP request.

<strong>Preflight Request:</strong>
OPTIONS /cors HTTP/1.1
Origin: http://x.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: X-Custom-Header
Host: y.com
Accept-Language: en-US
Connection: keep-alive
User-Agent: Mozilla/5.0...

<strong>Preflight Response:</strong>
Access-Control-Allow-Origin: http://x.com
Access-Control-Allow-Methods: GET, POST, PUT
Access-Control-Allow-Headers: X-Custom-Header
Content-Type: text/html; charset=utf-8

<strong>Actual Request:</strong>
PUT /cors HTTP/1.1
Origin: http://x.com
Host: y.com
X-Custom-Header: value
Accept-Language: en-US
Connection: keep-alive
User-Agent: Mozilla/5.0...

<strong>Actual Response:</strong>
Access-Control-Allow-Origin: http://x.com
Content-Type: text/html; charset=utf-8


<i>If the server wants to deny the CORS request, it can just return a generic response (like HTTP 200), 
without any CORS header. The server may want to deny the request if the HTTP method or headers requested 
in the preflight are not valid. Since there are no CORS-specific headers in the response, the browser 
assumes the request is invalid, and doesn’t make the actual request:</i>
<strong>Preflight Request:</strong>
OPTIONS /cors HTTP/1.1
Origin: http://x.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: X-Custom-Header
Host: y.com
Accept-Language: en-US
Connection: keep-alive
User-Agent: Mozilla/5.0...

<strong>Preflight Response:</strong>
// ERROR - No CORS headers, this is an invalid request!
Content-Type: text/html; charset=utf-8
</pre>
