# Changelog

## 1.0.0

**Release date:** TBD

Version 1.0.0 is the first release of `http_client`, which runs on Lus 2.0.

- Added the `http_client` package.
  - `http_client.new`: Creates a client with a base URL, default headers, retries, redirects, timeouts, and hooks.
  - `http_client.request`, `http_client.get`, and `http_client.post`: Send a request with a client that has the default options.
  - `http_client.is_error`: Returns true for an error object that `http_client` raised.
  - `client:request`: Sends a request with a JSON, URL-encoded, multipart, raw, or streamed body and returns the response.
  - `client:get`, `client:head`, `client:post`, `client:put`, `client:patch`, and `client:delete`: Send a request with that method.
  - `client:extend`: Creates a client that inherits the options of another.
  - `response:text` and `response:json`: Return the body of a response as a string or as decoded JSON.
  - `response:chunks` and `response:lines`: Return an iterator over the parts or the lines of a streamed response.
  - `response:close`: Closes the stream of a streamed response and its connection.
