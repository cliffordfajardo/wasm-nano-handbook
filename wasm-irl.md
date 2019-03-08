## What success stories are there of people using WASM?

Not too many at the moment - because it’s quite a new technology
Some of the interesting examples are coming from Mozilla, because they’re a big backer of WASM.

The interesting examples are where the complexities of JavaScript and WASM interfacing is minimised, because they’re doing very simple things. You won’t find people using WASM to work in React, or DOM manipulating applications.

16:25 A really interesting one that Mozilla published is part of our common toolchain was to assist with sourcemaps, a JS technology to map minified or transpiled code back to the original source.
16:40 It’s very widely used and very important for a lot of people.
16:45 Mozilla took the JavaScript used to generate sourcemaps, and ported it to web assembly and runs approximately three times faster.
16:55 From reading the blog post [https://hacks.mozilla.org/2018/01/oxidizing-source-maps-with-rust-and-webassembly/], it sounds like it will be released to production soon.
17:00 At the moment it’s being used for fairly specialised algorithmic tasks.
17:05 Web assembly is at the minimum viable product (MVP) stage and a young technology.
17:10 The feature set is deliberately minimal - as the feature set expands along with the toolchain and the ecosystem - we’ll start seeing it used for all sorts of things.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly
