# Short Response Questions

Answer each of these questions completely but concisely. Use the proper technical terminology. You may refer to the [Marcy Lab School Docs](https://marcylabschool.gitbook.io/marcy-lab-school-docs) or Google but do NOT copy and paste definitions or explanations verbatim.

You can earn up to 6 points for each response (3 points for writing quality, 3 points for technical content).

Before submitting your responses, use a spell checker / AI to ensure that you have no grammar or spelling mistakes.

## Question 1: Servers and HTTP

What is a server? Describe the HTTP request-response cycle including the key components of a request (method, endpoint, headers, body) and a response (status code, headers, body). Use an analogy to support your explanation.

**Your Answer:**

A server is any device, such as a computer, that stores, manages, and gives resources or data over the internet, listening for and responding to requests made by clients.
The HTTP request-response cycle begins when a client sends a request to a server using a URL. That request typically includes an HTTP method, such as ``GET``, ``POST``, ``PUT``, ``PATCH``, or ``DELETE``, which defines the intended action. It can also carry headers, which contain the request’s metadata, and a body, which holds additional data. It is used with methods like ``POST`` and ``PATCH``.

Once the server receives the request, it processes the request and sends back a response. That response includes a status code indicating the outcome, along with optional headers and a body containing content such as HTML or an image. The client then receives the response, interprets the status code, and can optionally cache or store the returned data.

This process is similar to ordering food at a restaurant. The client is the customer, and the server is the kitchen. The request is the order you place: the method represents the type of action (ordering, modifying, or canceling), the endpoint is the specific menu item, headers are special instructions, and the body is the detailed order. The response is the food you receive, along with a receipt (status code) indicating whether the order was successful.



## Question 2: Middleware

What is middleware in Express? How does it differ from a regular controller? Explain the role of `next()` and provide an example of when middleware is useful.

**Your Answer:**

Middleware is defined as a function that acts as an intermediary layer between requests and responses, using the next() method to pass control to the next function in the chain. It inspects, manipulates, and prevents requests and responses before the final controller is initiated to end the cycle.

For example, passing an argument such into next() would run control to the next middleware in the chain. If the next() method is not called, the cycle between the request and response would stop, and the final controller is never reached.



## Question 3: API Key Security

Why is it dangerous to use API keys in client-side (frontend) code? Explain how a backend server solves this problem (the "proxy" pattern). Include what role environment variables (`.env`) play in this approach.

**Your Answer:**

API Keys are credentials that verify your identity when sending a request to an API server. It allows the API provider to authenticate requests and control access to secured resources. Client-side frontend can easily expose the API key to unauthorized users through the developer tools, because all frontend code is visible in the browser, which would run the risk of having sensitive data being exposed.

Backend servers solve this through the proxy pattern. It forces the client to request data to the backend server, allowing sensitive data to have no visibility to the client, which allows sensitive data and server processes to be handled securely. Using a ``.env`` file helps store sensitive server-side data such as API Keys out of the codebase. For example, if the code is shared publicly on Github, the API key would not be exposed.

## Question 4: Debugging a Server

A fellow student is building an Express server. They send a `PATCH` request to `/api/bookmarks/1` using Postman, but they receive a `404` status code. List at least three things you would check to debug this issue and explain why each one could be the cause of the problem.

**Your Answer:**

1. First, I wouls make sure the server actually has a PATCH route defined for /api/bookmarks/:id. If the route doesn’t exist or is typed incorrectly (e.g. /api/bookmark/:id without the “s”), Express won’t match it and will return a 404.
2. Then, if a separate router file handles bookmark routes, I would check that it’s mounted correctly in the main server file (e.g. app.use("/api/bookmarks", bookmarkRouter)). A mismatch between the mount path and the route definition would cause Express to never find the route.
3.	Finally, I would make sure that the route is registered before any catch-all 404 middleware (e.g. app.use((req, res) => res.status(404).send("Not found"))). If the catch-all is defined first, it intercepts the request before Express ever reaches the PATCH route.​​​​​​​​​​​​​​​​