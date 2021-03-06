<a id="http-routing-java"></a>
# Routing DSL Overview

The Akka HTTP @ref[Low-Level Server-Side API](../server-side/low-level-server-side-api.md#http-low-level-server-side-api-java) provides a `Flow`- or `Function`-level interface that allows
an application to respond to incoming HTTP requests by simply mapping requests to responses
(excerpt from @ref[Low-level server side example](../server-side/low-level-server-side-api.md#http-low-level-server-side-example-java)):

@@snip [HttpServerExampleDocTest.java](../../../../../test/java/docs/http/javadsl/server/HttpServerExampleDocTest.java) { #request-handler }

While it'd be perfectly possible to define a complete REST API service purely by inspecting the incoming
`HttpRequest` this approach becomes somewhat unwieldy for larger services due to the amount of syntax "ceremony"
required. Also, it doesn't help in keeping your service definition as [DRY](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself) as you might like.

As an alternative Akka HTTP provides a flexible DSL for expressing your service behavior as a structure of
composable elements (called @ref[Directives](directives/index.md#directives-java)) in a concise and readable way. Directives are assembled into a so called
*route structure* which, at its top-level, can be used to create a handler `Flow` (or, alternatively, an
async handler function) that can be directly supplied to a `bind` call.

Here's the complete example rewritten using the composable high-level API:

@@snip [HighLevelServerExample.java](../../../../../test/java/docs/http/javadsl/server/HighLevelServerExample.java) { #high-level-server-example }

The core of the Routing DSL becomes available with a single import:

```java
import akka.http.javadsl.server.Directives.*;
```

Or by extending the `akka.http.javadsl.server.AllDirectives` class which brings together all directives into a single class
for easier access:

```java
extends AllDirectives
```

Of course it is possible to directly import only the directives you need (i.e. `WebSocketDirectives` etc).