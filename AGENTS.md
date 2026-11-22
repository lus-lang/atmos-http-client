# AGENTS.md

This repository, `lus-lang/atmos-http-client`, is the `http_client` package of the atmosphere registry. Programs load it with `require("https://atmosp.here/2.0/http_client.lus")`.

## Scope

Sends HTTP requests over `network.fetch` with a base URL, default headers, query tables, JSON, URL-encoded, and multipart bodies, retries with exponential backoff, redirects, and hooks. A response with a status of 400 or more raises an error object that carries the response. The public API is every function that `http_client.lus` returns in its module table. A change to that API needs a new entry in `CHANGELOG.md` and a version change in the header.

## Layout

- `http_client.lus` is the whole package. Its header doc comment carries the package metadata and the declared permissions.
- `tests/*_test.lus` are the tests. They load the package from the parent directory through `TEST_DIR`.

The tests load `form` from a checkout of `lus-lang/atmos-form` next to this repository, so clone it into the same parent directory first.

## Commands

```sh
lus test tests          # run the tests
lus check http_client.lus     # lint, including the package codes
lus doc http_client.lus       # print the reference
```

## Rules

- Every public function has a doc comment that states each result and each error, following `spec/design/style.md` of the Lus repository.
- The package never calls `pledge`. A new permission is declared in the header and in the README.
- Prose has no dashes and no semicolons, and never names the Roblox Lua dialect.
- Every bug fix comes with a test that fails without it.
