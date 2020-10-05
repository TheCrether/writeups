# Yawn1

[@TheCrether][1] and [@h4ckd0tm3][2]

## Description

```
yawn

<and an image of a panda>
```

## Solution

h4ckd0tm3 talked about maybe there being something in the header, so we looked into our browsers but there was nothing there.

Then I (TheCrether) thought, why not make the request with some kind of API testing tool, and used [https://reqbin.com/](https://reqbin.com/) because I had none installed at the time. For some reason, there now was a `Flag` Header included in the response.

The response was a `chunked` response. We found out that browsers don't handle chunked transfer encodings completely because they don't wait on the trailer headers.
https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Transfer-Encoding
Most tools for making HTTP requests also probably stop when the zero-length chunk arrives.

With openssl it also works when executing this command: `openssl s_client -connect okboomer.tasteless.eu:10401`
And then paste this content:

GET / HTTP/1.1
Host: okboomer.tasteless.eu

Flag: `tstlss{always keep looking}`

## Observations

When in the developer tools of our browsers, we looked into the network tab and there was nothing in the headers whatsoever.

### Misc

[1]: https://thecrether.at
[2]: https://schni.at
