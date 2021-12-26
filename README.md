# Hackney

<a href="https://github.com/gleam-lang/hackney/releases"><img src="https://img.shields.io/github/release/gleam-lang/hackney" alt="GitHub release"></a>
<a href="https://discord.gg/Fm8Pwmy"><img src="https://img.shields.io/discord/768594524158427167?color=blue" alt="Discord chat"></a>
![CI](https://github.com/gleam-lang/hackney/workflows/test/badge.svg?branch=main)

Bindings to Erlang's HTTP client, `hackney`.

```rust
import gleam/hackney
import gleam/http.{Get}
import gleam/should

pub fn main() {
  // Prepare a HTTP request record
  let req = http.default_req()
    |> http.set_method(Get)
    |> http.set_host("test-api.service.hmrc.gov.uk")
    |> http.set_path("/hello/world")
    |> http.prepend_req_header("accept", "application/vnd.hmrc.1.0+json")

  // Send the HTTP request to the server
  try resp = hackney.send(req)

  // We get a response record back
  resp.status
  |> should.equal(200)

  resp
  |> http.get_resp_header("content-type")
  |> should.equal(Ok("application/json"))

  resp.body
  |> should.equal("{\"message\":\"Hello World\"}")

  Ok(resp)
}
```

## Installation

```shell
gleam add gleam_hackney
```
