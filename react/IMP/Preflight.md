# What is a Preflight Request in the Browser?

A **preflight request** is an HTTP request sent automatically by the browser before the actual request, to check whether the server allows the actual request under Cross-Origin Resource Sharing (**CORS**) rules.

---

## Why is Preflight Needed?

Browsers enforce **same-origin policy**, which restricts requests between different origins (domain, protocol, or port).

When a request is considered **non-simple**, the browser sends a preflight request to verify if it is safe.

---

## When Does a Preflight Request Happen?

A preflight request is triggered when:

- The HTTP method is **not** GET, POST, or HEAD  
  (e.g., PUT, DELETE, PATCH)
- Custom headers are included  
  (e.g., `Authorization`, `X-Custom-Header`)
- The `Content-Type` is not one of:
  - `application/x-www-form-urlencoded`
  - `multipart/form-data`
  - `text/plain`

---

## How Preflight Works

1. The browser sends an HTTP **OPTIONS** request to the server.
2. The server responds with allowed methods, headers, and origins.
3. If allowed, the browser proceeds with the actual request.

---

## Example

### Preflight Request (OPTIONS)

OPTIONS /api/data HTTP/1.1
Origin: https://example.com

Access-Control-Request-Method: PUT
Access-Control-Request-Headers: Content-Type

### Server Response

HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://example.com

Access-Control-Allow-Methods: GET, POST, PUT
Access-Control-Allow-Headers: Content-Type

---

## Important CORS Headers

| Header                       | Description                           |
| ---------------------------- | ------------------------------------- |
| Access-Control-Allow-Origin  | Allowed origin(s)                     |
| Access-Control-Allow-Methods | Allowed HTTP methods                  |
| Access-Control-Allow-Headers | Allowed request headers               |
| Access-Control-Max-Age       | Cache duration for preflight response |

---

## Key Points

- Preflight requests use the **OPTIONS** method.
- They are automatically handled by the browser.
- They improve security by ensuring the server explicitly allows the request.
- They may add slight latency due to the extra round trip.

---

## Summary

A preflight request is a **safety check** performed by the browser before making certain cross-origin requests. It ensures the server permits the request based on CORS policies.
