CORS is between Browser and Server.<br>
Client initiates some HTTP request(from x.com domain) to back-end server(y.com). This fails SOP so browser follows CORS.  <br>
Browser sends PREFLIGHT req to Server (which is HTTP OPTIONS method) with ACCESS_CONTROL_REQUEST_METHOD header set  <br>
Server responds with all the headers ACCESS_CONTROL_ALLOW_XXXX set.  <br>
      (XXXX is --->  METHODS(GET,POST...), HEADERS, ORIGIN(hostnames or *) (and CREDENTIALS if cookies are enabled))  <br>
Browser checks if the client domain is part of ACCESS_CONTROL_ALLOWED_ORIGIN. If yes, Browser sends the actual HTTP request to the server.  <br>
Server responds back with the result of Client's HTTP request.
