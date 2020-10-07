**Guzzle, PHP HTTP client**

Guzzle is a PHP HTTP client that makes it easy to send HTTP requests and
trivial to integrate with web services.

- Simple interface for building query strings, POST requests, streaming large
  uploads, streaming large downloads, using HTTP cookies, uploading JSON data,
  etc...
- Can send both synchronous and asynchronous requests using the same interface.
- Uses PSR-7 interfaces for requests, responses, and streams. This allows you
  to utilize other PSR-7 compatible libraries with Guzzle.
- Supports PSR-18 allowing interoperability between other PSR-18 HTTP Clients.
- Abstracts away the underlying HTTP transport, allowing you to write
  environment and transport agnostic code; i.e., no hard dependency on cURL,
  PHP streams, sockets, or non-blocking event loops.
- Middleware system allows you to augment and compose client behavior.

## Sample

```c#
var client = new GuzzleHttp.Client(new PhpArray());
var res = client.request("GET", "https://api.github.com/user", new PhpArray()
{
    { "auth", new PhpArray() { "user", "pass" } },
});

Console.WriteLine((int)res.getStatusCode());    // "200"
Console.WriteLine(res.getHeader("content-type")[0].ToString()); // 'application/json; charset=utf8'
Console.WriteLine(res.getBody().ToString()); // {"type":"User"...'
```

```c#
// Send an asynchronous request.
var client = new GuzzleHttp.Client(new PhpArray());
var request = new GuzzleHttp.Psr7.Request("GET", "http://httpbin.org", new PhpArray());
var promise = client
    .sendAsync(request, new PhpArray())
    .then(new Action<GuzzleHttp.Psr7.Response>(response =>
    {
        Console.WriteLine($"I completed! {response.getBody().ToString()}");
    }));
//promise.wait();
```
