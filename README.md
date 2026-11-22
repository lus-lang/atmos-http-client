# http_client

`http_client` sends HTTP requests with `network.fetch` and adds a base URL, default headers, query tables, retries with exponential backoff, redirects, and hooks. A request body can be JSON, URL-encoded, multipart, or a stream that a coroutine produces. A response can be streamed, so that its body arrives in parts or line by line. A response with a status of 400 or more raises an error object that includes the response.

The following example calls the user API of a service with a bearer token and handles a missing user.

```lus nocheck
local http_client = require("https://atmosp.here/2.0/http_client.lus")

local api = http_client.new({
    base = "https://api.example.com",
    headers = { authorization = `Bearer $(token)` },
    retries = 3,
})

local user = api:get("/users/42", { query = { fields = "name" } }):json()
local created = api:post("/users", { json = { name = "Ada" } })
print(created.status, created.headers.location)

api:post("/avatars", { multipart = { user = "42", image = { filename = "avatar.png", data = bytes } } })

-- A status of 400 or more raises an error object with the response.
local ok, err = catch api:get("/users/0")
if not ok and http_client.is_error(err) and err.status == 404 then
    print(err.response:json().error)
end

-- A streamed response gives its lines as the server sends them.
for line in api:get("/events", { stream = true, timeout = 60 }):lines() do
    print(vector.tostring(line))
end
```

The package requires Lus 2.0 and declares the permission `network:http`, which it uses to send requests. It never calls `pledge`, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `http_client.lus`, which `lus doc http_client.lus` prints.
