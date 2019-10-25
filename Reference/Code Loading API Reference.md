## Code Loading API Reference

Castle's code loading API is a set of built in libraries consisting of:

- `network`: asynchronous HTTP networking, resource fetching with caching
- `require`: loading of Lua modules. Code can be fetched asynchronously over the network.
- `portal`: loading and management of Portals

All of these libraries are _globally available._ They do not need to be required in any Castle-run code.

### Network

#### `network.async(foo)`

Runs the function `foo` 'later', asynchronously with the caller. This is generally used when you want to perform I/O or other long operations from a performance-sensitive caller. The most common case is performing network I/O from a LÖVE event. If you don't wrap it in `network.async(...)`, it will still successfully perform the network request, but will pause the game while the request is happening.

Say you wanted to trigger a network request when the key 'k' is pressed. You could write the following:

```
function love.keypressed(key)
    if key == 'k' then
        network.async(function()
            local r = network.request('http://example.com')
            -- Will only get here once the request is completed
            -- `r` now contains the network response
        end)
        -- Code here runs immediately, doesn't wait for network response
    end
end
```

Asynchronous I/O is implemented by [Copas](http://keplerproject.github.io/copas/), so you can use all of its functions too, by bringing them into scope with `local copas = require 'copas'` (eg. you could get and save the current coroutine with `coro = coroutine.running()`, suspend it with `copas.sleep(-1)` and wake up the coroutine later with `copas.wakeup(coro))`. This is how `network.fetch` is itself implemented to handle simultaneous fetches. You usually don't have to use Copas directly unless you're writing some involved network code.

#### `network.request(...)`

This function has the same API (parameters and return values) as LuaSocket's [http.request function](http://w3.impa.br/~diego/software/luasocket/http.html#request), except it is asynchronous.

#### `network.fetch(url [, method])`

Fetches a resource from the `URL` url (a string) by HTTP, with Castle's caching behavior. `method` can be either `'GET'` or `'HEAD'`, and defaults to `'GET'`. If method is `'GET'`, returns the same values as `network.request(url)`, else returns the same values as `network.request { url = url, method = method }`. Is asynchronous.

The main reason to use this function over `network.request` above is that it caches the responses, so that repeated requests to the same `url` with the same `method` may resolve much faster after the first one.

#### `network.prefetch(urls [, baseUrl])`

Performs `network.fetch` on all `urls` (a Lua sequence of URL strings) asynchronously so that future `network.fetch` would have them cached. The results are not returned. If `baseUrl` is non-`nil`, prepends `baseUrl .. '/'` to non-absolute URLs in urls before prefetching them.

#### `network.flush(filter)`

Flushed all entries of the network.fetch cache that pass the filter. filter should be a function takes one parameter, url, which is the URL that the cache entry points to, and returns a truthy value if and only if that entry should be removed from the cache.

#### `network.isAbsolute(url)`

Whether the string `url` represents an absolute URL.

#### `network.exists(url [, skipCache])`

Whether the URL `url` points to a resource that exists (gives an HTTP 200 code on a `'HEAD'` request). If `skipCache`, ignores the fetch cache while making the `'HEAD'` request.

#### network.status(url [, method])

Status of `network.fetch` for this `url`, `method` combination. `method` defaults to `'GET'`. Returns `'none'` if not cached (either never fetched, error'd or flushed from cache), `'fetching'` if currently being fetched (asynchronously), or `'fetched'` if fetched and cached.

### require

The require library has only one function, named require:

#### require(path [, opts])

- If `path` names a module included with Castle, works like Lua's built-in `require`, else...

- If `path` begins with `'http://'` or `'https://'` (an "absolute" path), the text returned by a HTTP `'GET'` to that URL, or that URL followed by `'.lua'` or `'/init.lua'` (whichever is the first one to return a "200 ok" `'HEAD'` response) is used as the source code of the module, then that source code is `require`d normally. Then, the directory of that URL (without the last path element) is used as the 'base URL' for transitive `require`s from that module (unless overridden by a new absolute path).

- If path is not "absolute", attempts to resolve path as a "relative" path. The resolution occurs by first replacing all '.'s with '/'s, as in normal Lua require, then appending that path to the base URL of the calling module, followed by nothing or '.lua' or '/init.lua' (whichever is the first one to satisfy network.exists). The text returned by a HTTP 'GET' to that URL is used as the source code of the module and required normally.
  In the case of a require from the network, the key set in package.loaded is the final URL that the code was loaded from. Network requires are performed with network.fetch, thus giving Castle's caching behavior.

`opts` is optional, and can have the following keys:

- `saveCache` — whether to save this module in `package.loaded`. (default `true`)

- `noEval` — whether to skip loading the module. Useful to only perform the lookahead (see below). (default `false`)

- `basePath` — the 'base URL' for relative `require`s. (defaults to the base URI given by the calling module)

- `parentEnv` — the global environment of the module calling require — used to look up package. (defaults to the global environment of the calling module)

- `childEnv` — the global environment to set as the module being `require`d. (defaults to what parentEnv)

- `preamble` — a string of code to prepend to the module's code before loading. (defaults to `''`)

In addition to all this, the loaded code is parsed for `require`s or other LÖVE resource-loading functions that are passed static string URIs and those resources are simultaneously pre-fetched so that future fetches are quicker.

### portal

The `portal` global variable refers to the current Portal that code is running in. Portals manage the lifetime, event forwarding and drawing for a set of modules. Each Portal maintains a separate global environment so that they can load modules that maintain state without interfering with each other.

#### `portal:newChild(path, [args])`

Create a new child Portal of the current Portal. `path` is a path that can be passed to `require`. The module at `path`, and the modules it requires, are loaded with a new global environment created for that portal. Potentially performs network I/O to fetch the modules and data the child portal requires, so run inside a `network.async(...)` block if in a performance-sensitive caller. Returns the child portal, on which you can call the functions below.

```
child:directorydropped(...)
child:draw(...)
child:filedropped(...)
child:focus(...)
child:keypressed(...)
child:keyreleased(...)
child:lowmemory(...)
child:mousefocus(...)
child:mousemoved(...)
child:mousepressed(...)
child:mousereleased(...)
child:quit(...)
child:resize(...)
child:textedited(...)
child:textinput(...)
child:threaderror(...)
child:touchmoved(...)
child:touchpressed(...)
child:touchreleased(...)
child:update(...)
child:visible(...)
child:wheelmoved(...)
child:gamepadaxis(...)
child:gamepadpressed(...)
child:gamepadreleased(...)
child:joystickadded(...)
child:joystickaxis(...)
child:joystickhat(...)
child:joystickpressed(...)
child:joystickreleased(...)
child:joystickremoved(...)
```

Each of these methods shares a name with a [LÖVE callback](https://love2d.org/wiki/love#Callbacks). Calling that method calls the global `love.{name}(...)` function defined inside the child Portal, passing all of the given arguments to the function. This way, the child function's LÖVE callbacks can be triggered from the parent with full control. Child Portals do not receive events by default, the parent has to explicitly trigger the events.
