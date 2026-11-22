# http_client

Sends HTTP requests over `network.fetch` with a base URL, default headers, query tables, JSON, URL-encoded, and multipart bodies, retries with exponential backoff, redirects, and hooks. A response with a status of 400 or more raises an error object that carries the response.

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

api:post("/avatars", { multipart = { user = "42", image = { filename = "a.png", data = bytes } } })

-- A status of 400 or more raises an error object with the response.
local ok, err = catch api:get("/users/0")
if not ok and http_client.is_error(err) and err.status == 404 then
    print(err.response:json().error)
end
```

The package requires Lus 2.0. It needs `network:http` to send requests. It calls no `pledge` of its own, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `http_client.lus`. Run `lus doc http_client.lus` to print it.
