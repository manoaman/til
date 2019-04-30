### Forward and Redirect

Redirect:
```
Redirect sets the response status to 302 [1], and the new url in a Location header, and sends the response to the browser. Then the browser, according to the http specification, makes another request to the new url.
```

Forward:
```
Forward happens entirely on the server. The servlet container just forwards the same request to the target url, without the browser knowing about that. Hence you can use the same request attributes and the same request parameters when handling the new url. And the browser won't know the url has changed (because it has happened entirely on the server).
```

https://stackoverflow.com/questions/6068891/difference-between-jsp-forward-and-redirect
https://www.baeldung.com/servlet-redirect-forward
