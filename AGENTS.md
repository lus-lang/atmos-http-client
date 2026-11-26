# AGENTS.md

`lus-lang/atmos-http-client` is the repository of the `http_client` package of the atmosphere registry. Programs load the package with `require("https://atmosp.here/2.0/http_client.lus")`.

## Scope

`http_client` sends HTTP requests with `network.fetch` and adds a base URL, default headers, query tables, retries with exponential backoff, redirects, and hooks. A request body can be JSON, URL-encoded, multipart, or a stream that a coroutine produces. A response can be streamed, so that its body arrives in parts or line by line. A response with a status of 400 or more raises an error object that includes the response. The public API is every function that `http_client.lus` returns in its module table. A change to that API needs a new entry in `CHANGELOG.md` and a version change in the header.

## Layout

- `http_client.lus` is the whole package. Its header doc comment contains the package metadata and the declared permissions.
- `tests/*_test.lus` are the tests. They load `http_client.lus` from the parent of `TEST_DIR`, the directory that holds the test file.

The tests load `form` from a checkout of `lus-lang/atmos-form` next to this repository, so clone it into the same parent directory first.

## Commands

Run these commands from the root of the repository.

```sh
lus test tests          # run the tests
lus check http_client.lus     # lint, including the package codes
lus doc http_client.lus       # print the reference
```

## Rules

- Every public function has a doc comment that states each result and each error, following `spec/design/style.md` of the Lus repository.
- The package never calls `pledge`. A new permission is declared in the header.
- Prose follows the `lus-writing` skill, which `lus agents init` installs and https://lus.dev/agents/skills/lus-writing/SKILL.md serves. In particular, prose has no dashes or semicolons and never names the Roblox Lua dialect.
- Every bug fix comes with a test that fails without it.
