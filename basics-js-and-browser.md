## Performance - sizes

TBD

## A short browser history

- 1995: /index.html = static HTML content
- 2005: /index.php = dynamic content generated from server-side code
- TODAY: /api/v1/todos = semi-raw data in a browser-understandable format

So far JS was the only language that could be run by browsers ; it was mostly designed for user interactions, but now we can build fully-fledged apps with it
--> How to make it faster?

- use a framework
- precompile: TypeScript, Dart

Wait. Can a webpage run at hardware-native speed?
Yes, With WASM.

source: https://fosdem.org/2019/schedule/event/the_state_of_webassembly_in_2019/

## Where did JavaScript come from?

Prior to JS, the web was a very static place: If you wanted to create interactivity in the browser, it involved a round-trip to the server.

JS was designed to support a modest amount of interactivity client-side, such as form validation.

So JS was developed in a short space of time, and everyone knows it’s a bit of a quirky language. Browser makers spend a lot of time testing to make sure changes don’t break existing websites.

No one expected it to become as fundamental as it has become.

JS has become a runaway success - not just within the browser, but extensively on the mobile or smart watches. You can run JavaScript programs anywhere.
JS is now very mature - it’s evolving at a rapid space. When new language features come along, transpilers can be used to backport those features into older versions of JavaScript.

## Prerequisite: main building blocks of a browser

what happens at runtime? what gets loaded onto the browser, what gets executed, and by what????

When a browser receives JS code, it needs to execute it.
But JS is a high-level language, that the computer doesn't understand as is.

Need for a JS ENGINE (also referred to as a COMPILER): a program that takes human-readable source code (in our case JavaScript), and from it generates machine-readable instructions (= MACHINE code = NATIVE code) for your computer.
"Compiling" in the browser context implicitely means "compiling to MACHINE CODE".

In the past:
Before V8 and other compilers, Javascript was interpreted (= dealt with by interpreter). That was slow.

Now:
From 2012 on, browsers have been implementing new Javascript engines, trying to COMPILE some portions of code, to speed Javascript up. Most browsers today do high-perf, optimized JIT (just-in-time) compiling.

For example, V8 is Google’s open source high-perf JavaScript and WebAssembly engine. It's written in C++ and implements ECMAScript and WebAssembly. V8 can run standalone or embedded into any C++ application ; it's used in Google Chrome, Node.js and others.

Sources:
https://v8.dev/
https://stackoverflow.com/questions/21571709/difference-between-machine-language-binary-code-and-a-binary-file

### Disambiguation: engine vs VM

An engine, like V8, is a type of VM.
A runtime is a VM ; i.e. everything needed for the code to run.

- What happens when I run C code on my computer? And rust code? and JS code? what's compiled, what's not, what uses a vm?
-

### Zoom: what an engine does

Actually, an engine is more than just a compiler. Hdere's what it does.

With JS code:

With webassembly code:

## JS

JS is a non-blocking single-threaded language.
It's run in non-blocking, asynchrony-enabling environements.

## How browsers work

### The inner workings of a browser lens: Building blocks:

- JS engine = V8 = chrome's runtime = node's runtime <-- that's the part we're interested in.  
  V8 has a (call) stack (for execution contexts, where the stack frames are - just one because one thread => one call stack. It records where in the program we are. If we step into a function we push, if we return we pop off.) and a heap (for memory allocation). If the stask has stuff on it, it's stuck. We don't want that, that freezes the UI.

- event loop: provided by the browser
- callback queue: provided by the browser
- web APIs: DOM, ajax, setTimeOut...

see https://www.youtube.com/watch?v=8aGhZQkoFbQ 3:36 and 12:57 for diagrams

NB: V8 is the engine that's used both in node and the browser. In node, the event loop is provided by libuv.

### The architecture lens

rendering engine, memory, UI etc
// TBD diagrams

### The thread lens: Threads and processes

https://developers.google.com/web/updates/2018/09/inside-browser-part1

// TBD diagrams

### URL to interactive

https://medium.com/@maneesha.wijesinghe1/what-happens-when-you-type-an-url-in-the-browser-and-press-enter-bb0aa2449c1a and https://developers.google.com/web/updates/2018/09/inside-browser-part2

_(User starts typing maps.google.com into the browser address bar)_

#### 1. Handle input

The UI thread asks is "Is this a search query or URL?". In Chrome, the address bar is also a search input field, so the UI thread needs to parse and decide whether to send you to a search engine, or to the site you requested.

_(User hit enter)_

#### 2. Start navigation

- loading spinner is displayed
- to get site content, the UI thread initiates a network call

#### 3. Connect

The network thread takes care of the connection.

- In order for my computer to connect with the server that hosts maps.google.com, I need the IP address of maps.google.com. DNS(Domain Name System) is a DB that maintains the name of the website (URL) and the particular IP address it links to. Every single URL on the internet has a unique IP address assigned to it. The IP address belongs to the computer which hosts the server of the website we are requesting to access. For an example, www.google.com has an IP address of 209.85.227.104. DNS is a list of URLs and their IP addresses just like how a phone book is a list of names and their corresponding phone numbers. So:

  - check the cache for a DNS record to find the corresponding IP address of maps.google.com: Browser Cache, OS cache, router cache, ISP cache.
  - If the requested URL is not in the cache, ISP’s DNS server (=DNS Recursor) initiates a DNS query to find the IP address of the server that hosts maps.google.com. The purpose of a DNS query is to search multiple DNS servers on the internet until it finds the correct IP address for the website.

- Once the IP address is found, the browser initiates a TCP connection with the server that matches IP address, in order to transfer information. This connection is established using a process called the TCP/IP three-way handshake. This is a 3-step process where the client and the server exchange SYN(synchronize) and ACK(acknowledge) messages to establish a connection. These messages are sent using small data packets.

_(TCP connection is established)_

#### 4. Request

The browser sends an HTTP request to the web server (usually GET, or POST). This request will also contain additional information such as browser identification (User-Agent header), types of requests that it will accept (Accept header), and connection headers asking it to keep the TCP connection alive for additional requests. It will also pass information taken from cookies the browser has in store for this domain.

_(Server handles the request and sends back an HTTP response.
The server contains a web server (i.e Apache, IIS) which passes the request to a request handler. The request handler is a program (in ASP.NET, PHP, Ruby, etc.) that reads the request (+headers/cookies) to check what is being requested and also update the information on the server if needed. Then it will assemble a response in a particular format (JSON, XML, HTML). The server response contains the web page you requested as well as the status code (1xx = info, 2xx = success, 3xx = redirect, 4xx = client error, 5xx = server error), compression type (Content-Encoding), how to cache the page (Cache-Control), any cookies to set, privacy information, etc._
)

#### 5. Read response

Once the response body (payload) starts to come in, the network thread looks at the first few bytes of the stream if necessary.

The response's Content-Type header should say what type of data it is, but since it may be missing or wrong, MIME Type sniffing is done here.

Also some security checks.

If the response is an HTML file, then the next step would be to pass the data to the renderer process, but if it is a zip file or some other file then that means it is a download request so they need to pass the data to download manager.

_(Once all of the checks are done and Network thread is confident that browser should navigate to the requested site, the Network thread tells UI thread that the data is ready.)_

#### 6. Find a renderer process\*

UI thread then finds a renderer process to carry on rendering of the web page.  
\*In reality, this is started at step 2 for optimization.

#### 7. Commit navigation

An IPC is sent from the browser process to the renderer process to commit the navigation. It also passes on the data stream so the renderer process can keep receiving HTML data. Once the browser process hears confirmation that the commit has happened in the renderer process, the navigation is complete and the document loading phase begins.  
At this point, address bar is updated and the security indicator and site settings UI reflects the site information of the new page. The session history for the tab will be updated so back/forward buttons will step through the site that was just navigated to. To facilitate tab/session restore when you close a tab or window, the session history is stored on disk.

#### 8. Render

Critical rendering path as the sequence of steps the browser goes through to turn “the code and resources required to render the initial view of a web page” into a visible browser output.

Steps:

- Build DOM, visible content only (Note: The browser builds up the DOM incrementally. That means it can start to parse the HTML as soon as the first chunks of the code come in and it will then add nodes to the tree structure as needed. So: HTML is render blocking, but it's OK because the DOM can be built incrementally.) When the HTML parser encounters a script tag, it pauses its process of constructing the DOM and yields control to the JavaScript engine; after the JavaScript engine finishes running, the browser then picks up where it left off and resumes DOM construction. When it encounters a link: same, it loads the resource.

- Build CSSOM, visible content only (BUT the CSSOM cannot be built incrementally like the DOM. Imagine if there was a third line in the stylesheet, for example p { font-weight: normal; }, which overrides the first p declaration. So we have to wait until all the CSS is downloaded and processed before we can move on with the rendering step. CSS is RENDER blocking.)

- JS roundtrips

- Render: build the render tree (CSSOM+DOM)
- Layout: computes the exact position and size of each object.
- Paint: takes in the final render tree and renders the pixels to the screen.

Schema

https://developers.google.com/web/fundamentals/performance/critical-rendering-path/images/analysis-dom-css-js.png

(https://developers.google.com/web/fundamentals/performance/critical-rendering-path/images/analysis-dom-css-js-async.png)

is script is async: the only blocking thing now is the CSS

- JS blocks DOM construction ie is PARSER blocking. Because: it can both change the DOM and CSSOM, so the parser has to stop its work until the script is fully executed.

Fix: In an optimal case, you drop JS all together for the initial rendering of the page. If that is not possible:

- put the script tag to the bottom of the page, just before the closing </body> tag // Doing so, the script is loaded and executed after all the page is already parsed and loaded
- Use DEFER or ASYNC. (make only sense when using the script in the head portion of the page) An asynchronous script has several advantages:
  The script is no longer parser blocking and is not part of the critical rendering path. Because there are no other critical scripts, the CSS doesn't need to block the domContentLoaded event. The sooner the domContentLoaded event fires, the sooner other application logic can begin executing.

* CSS:

  - is RENDER blocking because needed for the CSSOM.
  - CSSOM blocks JS execution ie is SCRIPT blocking. Because: JS might ask for an element’s color. So the CSSOM has to be present before the script can be run. CSS is therefore also SCRIPT blocking.

    Fix: get it to the client as soon and as quickly as possible to optimize the time to first render. Make sure all the CSS link tags are in the head of your HTML code so the browser can dispatch the requests immediately. Another strategy is to lower the amount of render blocking CSS with media queries.

Other fix: minimize the Bytes that Go Down the Network: minify, compress, cache

DOM events:

- DOMContentLoaded event fires when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading. Synchronous JavaScript pauses parsing of the DOM. If you want the DOM to get parsed as fast as possible after the user has requested the page, you can make your JavaScript asynchronous and optimize loading of stylesheets. If loaded as usual, stylesheets slow down DOM parsing as they're loaded in parallel, "stealing" traffic from the main HTML document.
- load: should be used only to detect a fully-loaded page. Emitted when a resource and its dependent resources have finished loading.

Other APIs:

- Is it happening? First Paint (FP) / First Contentful Paint (FCP)
- Is it useful? First Meaningful Paint (FMP)
- Is it usable? Time to Interactive (TTI)

https://developers.google.com/web/fundamentals/performance/user-centric-performance-metrics

Script types:
See https://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html +++

async (! not working for inline scripts)
the browser should, if possible, load the script asynchronously.
Browsers usually assume the worst case scenario and load scripts synchronously, (i.e. async="false") during HTML parsing.

defer (! not working for inline scripts)
the script is meant to be executed after the document has been parsed, but before firing DOMContentLoaded.
Scripts with the defer attribute will prevent the DOMContentLoaded event from firing until the script has loaded and finished evaluating.
This attribute must not be used if the src attribute is absent (i.e. for inline scripts), in this case it would have no effect.
To achieve a similar effect for dynamically inserted scripts use async="false" instead. Scripts with the defer attribute will execute in the order in which they appear in the document.

Src:
https://www.sitepoint.com/optimizing-critical-rendering-path/
https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css

RequestAnimationFrame:  
Requests an callback (whatever it is, but obvisouly we use it for animations) to be called just before a render (+ layout + paint) event.
https://flaviocopes.com/requestanimationframe/

#### 9. Initial load complete

Once the renderer process "finishes" rendering, it sends an IPC back to the browser process (this is after all the onload events have fired on all frames in the page and have finished executing). At this point, the UI thread stops the loading spinner on the tab.

I say "finishes", because client side JavaScript could still load additional resources and render new views after this point.

### How V8 works

https://cdn-images-1.medium.com/max/1200/1*ZIH_wjqDfZn6NRKsDi9mvA.png

also see Lin Clark's talk

### Runtime

Rendering path

- ! requestAnimation frame

multiple renderer process

running JavaScript is the main thread's job
