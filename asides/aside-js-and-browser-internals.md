# How browsers work

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/angle.jpg">  
  <div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

Between the moment you type a URL in your browser and the moment the page is displayed and usable, a lot is going on.  
You might have heard the expression "URL to interactive" - it refers to all these steps that happen after you enter a URL.  
But once you're using the web app, there is _still_ a lot going on: rendering, JS execution, etc. And what if you open a new tab? And what happens if there are a lot of UI animations?

Many excellent resources detail the different steps of URL to interactive, but I was always missing an overview. To get a holistic view of how browsers run web apps, we need to look at this from **multiple angles**. Each of them represents a specific aspect of the reality.  

Let's go!

* The architecture lens
* JS and the engine lens (which browser uses what etc.)
* The rendering path lens
* The processes lens
* Sumup: URL to interactive

## Prerequisite: a short browser history

* 1995: /index.html = static HTML content
* 2005: /index.php = dynamic content generated from server-side code
* TODAY: /api/v1/todos = semi-raw data in a browser-understandable format

So far JS was the only language that could be run by browsers; it was mostly designed for user interactions, but now we can build fully-fledged apps with it.
--> How to make it faster?

* Use a framework
* Precompile: TypeScript, Dart

Wait. Can a webpage run at hardware-native speed?
Yes, With WASM.

Source: https://fosdem.org/2019/schedule/event/the_state_of_webassembly_in_2019/

## Architecture

### Building blocks of a browser

1. Transform HTML and other resources of a web page into an interactive visual representation on a user's device

* Rendering engine = layout engine = browser engine, provided by the browser
NB: In addition to layout and rendering, a browser engine enforces the security policy between documents, handles navigation through hyperlinks and data submitted through forms, and implements the Document Object Model (DOM) data structure.

2. Run JS and use Web APIs

* JS engine e.g. V8 for chrome, this includes garbage collection
* Event loop, provided by the browser (aka it's not in V8!)
* Callback queue, provided by the browser (aka it's not in V8!)
* Web APIs: DOM, ajax, setTimeOut... coming from the environment

3. Others

* Networking, Data and other logics

NB: JS was originally created for use in browsers, but it is now used elsewhere too. So the implementation of JS engines is decoupled from browser engines. The two engines work in concert via the shared DOM data structure.

### Different browsers, different engines

* Chrome (and its open source sibling Chromium): V8 + Blink
* Edge: soon V8 + Blink
* Firefox: SpiderMonkey + Gecko
* Safari: Nitro + WebKit
NB: Chrome initially used the WebKit rendering engine but forked in 2013 to create their own, Blink. V8 is the JS engine that's used both in node and the browser. In node, the event loop is provided by libuv.

## JS and the engine

### Where did JS come from?

JS is the language of the web. It's a high-level language run in single thread in in non-blocking, asynchrony-enabling environements.

Prior to JS, the web was a very static place: iif you wanted to create interactivity in the browser, it involved a round-trip to the server.
JS was designed to support a modest amount of interactivity client-side, such as form validation.
So in 1995, Brendan Eich developed JS for Netscape in a short time.
No one expected it to become as fundamental as it has become.
JS has become a runaway success:

* All browsers can run JS
* This went much further: engines are now embedded in many other types of host software, JS is also used in the backend. You can run JS programs anywhere like on smart watches.

Everyone knows JS started off as a bit of a quirky language. Browser makers spend a lot of time testing to make sure changes don’t break existing websites.
JS is now very mature - it’s evolving at a rapid space. When new language features come along, transpilers can be used to backport those features into older versions of JS.

JS is high-level which means it’s human readable - surely methods like “filter” or “fetch” are understandable in human language. 
It’s dynamically typed which makes it very flexible.

### Terminology

Runtime = VM = everything needed for the code to run.
An engine is a type of VM.
JS engine = a VM than can run JS.

### About V8

V8 is Google's JS and Wasm engine.
It's open source and written in C++.

V8 is used in Chrome and other chromium-based browsers such as Opera and soon Edge.
V8 is also used in other embedders such as Node.js and Electron. 
V8 can run standalone or embedded into any C++ application.


V8 has:

* A (call) stack // It records where in the program we are, keeps track of execution contexts (stack frames). If we step into a function we push a new frame onto the stack, if we return we pop off it. In V8 there's just one stack because one thread => one call stack.
* A heap // for memory allocation. If the stack has stuff on it, it's stuck. We don't want that, that freezes the UI.

### How the JS engine runs JS code

You as a human write JS code, that's high-level. At some point later in time, your code needs to be executed on a user’s machine. But the machine/CPU doesn't understand high-level language, it needs low-level instead. So if you just ship JS to the user’s machine and it runs, something must happen in between, right? Well, that’s the job of your JS engine that's in your browser: it will take care of execution and translation.
The JS ENGINE (=COMPILER) is a program that takes human-readable source code, in our case JS, and from it generates machine-readable instructions (= MACHINE code = NATIVE code) for your computer.
"Compiling" in the browser context implicitely means "compiling to MACHINE CODE".

So, how exactly does that work?

Let’s take the example of V8, which is chrome’s browser engine.

* When receiving JS code, the engine first parses the code and transform it in a less human-readable but more structured representation: the abstract syntax tree (AST).
* Then, two things might happen:
  * Either your code is translated line by line into some code that is close to machine code, and then executed as such. That’s the job of Ignition = the baseline compiler = the interpreter. But the machine code generated line by line from the bytecode is not optimized. So what if some portion of your code is run over and over again (like the React diffing algo; such code is called "hot" because it;'s run again)? then we’re running over and over some code that is not really optimized?
  * No. That’s where the optimizing compiler comes in. The optimimizing compiler is called Turbofan in v8. Turbofan transforms hot codes into actually super efficient machine code. Maybe you’ve heard about JIT compiling (just in time) - that’s what it is. So, Ignition (baseline compiler) starts fast but runs code slowly, and Turbofan (optimizing compiler) takes longer to generate code but can run it really fast.

NB:
    * Note that there this is not sequential, this happens by chunks: run, observe, optimize, run... Optimization relies on assumptions on the types of your JS objects. Assumptions can be wrong! optimize/deoptimize cycles
    * One more thing that also takes time (although it’s on another thread): GC
    * Before V8 and others, JS was only interpreted (= managed by interpreter). That was slow. From 2012 on, browsers have been implementing new JS engines to COMPILE some portions of code; it speeded JS up. Most browsers today do high-performance, optimized JIT (just-in-time) compiling.
    * In v8 there’s a new, dedicated component that takes care of wasm. It’s called LiftOff, a streaming compiler. LiftOff generates wasm code as soon as it receives it. Then your code can be executed. Additionally, if your wasm code is hot, it will be passed to Turbofan for optimization, just like for JS.

Sources:
https://v8.dev/
https://stackoverflow.com/questions/21571709/difference-between-machine-language-binary-code-and-a-binary-file


<p align="center">
<img width="820" src="https://user-images.githubusercontent.com/9762897/72212473-287e3d00-34dd-11ea-9141-95aa4264f9da.png">  
  <div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

<p align="center">
<img width="520" src="https://user-images.githubusercontent.com/9762897/72212505-e0134f00-34dd-11ea-9c7c-82e58adbad9f.png">  
  <div align="center"><sub><sup>JS run steps - Lin Clark https://hacks.mozilla.org/2017/02/what-makes-webassembly-fast/</sup></sub></div> 
</p>

<p align="center">
<img width="280" src="https://user-images.githubusercontent.com/9762897/72212507-e275a900-34dd-11ea-8e44-cfcfe9986950.png">  
  <div align="center"><sub><sup>WASM run steps - Lin Clark https://hacks.mozilla.org/2017/02/what-makes-webassembly-fast/</sup></sub></div> 
</p>

Sources:

* https://hacks.mozilla.org/2017/02/what-makes-webassembly-fast/
* ++++++ https://softwareengineeringdaily.com/2018/09/26/javascript-engines-with-mathias-bynens/ 

## Processes

Chrome is special because it has one process per tab.

<p align="center">
<img width="520" src="https://user-images.githubusercontent.com/9762897/72212586-f372ea00-34de-11ea-9f42-a51a93e5fc10.png">  
  <div align="center"><sub><sup>Mariko Kosaka https://developers.google.com/web/updates/2018/09/inside-browser-part1</sup></sub></div>
</p>

Sources:

* ++++++ https://developers.google.com/web/updates/2018/09/inside-browser-part1
* ++++++ https://softwareengineeringdaily.com/2018/06/28/chrome-and-chromium-with-david-bokan/


## URL to interactive

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

if script is async: the only blocking thing now is the CSS

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

## Zoom on performance

170kB

### DOM events

* `DOMContentLoaded` fires when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading. Synchronous JavaScript pauses parsing of the DOM. If you want the DOM to get parsed as fast as possible after the user has requested the page, you can make your JavaScript asynchronous and optimize loading of stylesheets. If loaded as usual, stylesheets slow down DOM parsing as they're loaded in parallel, "stealing" traffic from the main HTML document.
* `load` fires when a resource and its dependent resources have finished loading. Should be used only to detect a fully-loaded page.

### APIs

* Is it happening? First Paint (FP) / First Contentful Paint (FCP)
* Is it useful? First Meaningful Paint (FMP)
* Is it usable? Time to Interactive (TTI)

https://developers.google.com/web/fundamentals/performance/user-centric-performance-metrics

## Questions

* What happens when I run C code on my computer? And rust code? and JS code? what's compiled, what's not, what uses a vm?
* What happens at runtime? what gets loaded onto the browser, what gets executed, and by what?

## Notes

TBD insert my diagrams and sources
See https://www.youtube.com/watch?v=8aGhZQkoFbQ 3:36 and 12:57 for diagrams
https://cdn-images-1.medium.com/max/1200/1*ZIH_wjqDfZn6NRKsDi9mvA.png
also see Lin Clark's talk
Whats the main thread in there?

Rendering path
- ! requestAnimation frame
multiple renderer process
running JavaScript is the main thread's job

<img src="https://cdn-images-1.medium.com/max/2600/1*PiFyb7IV8vTDCGEeUOWLVQ.jpeg"/>  
Source: https://medium.com/@francesco_rizzi/javascript-main-thread-dissected-43c85fce7e23
