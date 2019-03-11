## WASM WebGL?

They are rather unrelated, but can be used together.

WebGL is a browser's API onto the machine's GPU (= graphical processing unit = 3D hardware). It's based on the OpenGL standard.

Web developers can use JS/WASM/... to access WebGL when they need to do 3D graphics fast.

More: https://getpocket.com/a/read/2365657803

## WASM vs ASM and PNaCl

ASM and PNaCl paved the way for WASM.

- Portable Native Client (PNaCl) (Google): compile to safe native for C & C++ in browsers. Was never even fully enabled in Chrome, use cases: Google+ had an image editor.

- ASM (Mozilla): PoC of a low-level virtual machine built out of JavaScript. They took a very strict subset of the language, built into their own browser something that understood the language they’d created, and optimised for it. Was demonstrated at Mozilla in partnership with the gaming companies like Epic Games (with Unreal Engine) and Unity (Unity engine and IDE). It got successful: once ASM.js crossed over into other browsers, it became clear that it was gonna cross over into all the browsers.

PNaCl is not gonna go cross-browser, but a lot of the work was LLVM based. It was getting ahead of what we did with ASM.js, so it’s the perfect marriage now. It was originally considered ill-starred, but it’s actually turning out great to have people working on WebAssembly who used to work on ASM.js and PNaCl.

ASM and WASM are similar - they define an assembly-like set of instructions.
Limitations of ASM.js:

- it is coded in JavaScript so is quite verbose and difficult to understand syntax.
- ASM.js is (a subset) of JS => still need to parse JS
- ... but probably need to run a dedicated parser for that subset ; costly parsing problem compared to what could be done with a more efficient, compressed abstract syntax tree (AST), which is what WebAssembly is aiming at.
- In addition, it is only optimised for Firefox (?).

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## How is WASM different from writing, say, Flash?

3:35 Part of the reason why people think it sounds similar is because one of the motivations of creating WASM is to create a new assembly language which is a compilation target for a range of high level languages.
3:50 So C#, Java, Rust, C++ and others are now able to be compiled into WASM and run in the browser.
4:00 That immediately makes people think of how they used to be able to run those kind of languages in the browser.
4:05 There are some very fundamental differences in the way this is being achieved.
4:15 Flash, Silverlight and so on used the plugin model, which is a bolt-on to the side of the browser that lets you have a different execution environment and a restrictive API to communicate between that runtime and the first-class runtime in the browser.
4:30 Web assembly isn’t like that; it is very tightly integrated within the JavaScript virtual machine, and there’s a very close synergy between the two.
4:45 The other difference is in the way it was created.
4:50 Silverlight was an invention pushed by Microsoft; Flash was an Adobe creation [ed: FutureWave created Flash, who were then acquired by Macromedia and then subsequently Adobe].
5:00 They were created in an era of competition, and they were different plugin vendors and browsers.
5:10 Web assembly was created through collaboration, with significant representation from browser vendors.
5:20 That has a significant impact on its adoption; it’s been adopted and moved into production browsers in a very short space of time.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## is WASM a JS killer?

No - maybe in a veeeery long time.

A cute feature of the logo is that the notch in the top enables it to connect with the JavaScript logo.

Early stage adopters of WASM are going to use it because of the speed advantages it offers, and its ability to port existing programs to the web, rather than as a rejection of JavaScript. As we move on, however, it should be possible to write in whatever language you like, compile it to WASM, and run it in any browser. This is seen by many as a future world in which JavaScript no longer rules the web. Is this likely? There is a great deal of investment in JavaScript and WASM is designed to run on the same engine that runs it, so it isn't going to be disadvantaged by the adoption of WASM. At the moment WASM still needs JavaScript to do things like interact with DOM and this makes it a partnership. If a JavaScriptless future is going to be a reality then WASM has to be expanded a lot, and this might not happen if interworking with JavaScript is a cheaper option. It really might turn out to be a partnership rather than a takeover.
https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html

# FAQ

## Is WASM ready for production use?

It’s called assembly - if you look at the way that PIC micro-controllers and 6502 processors, it’s very similar - none of them understand strings.
It doesn’t mean that you can’t write applications just because the processor doesn’t have an innate understanding of what a String is.
It just means that most people won’t write the assembly language directly; they’ll rely on a compiler where someone else has done all the magic.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## Doesn’t the advent of WASM mean that we will see larger binaries being delivered to clients?

Good question - because if a desktop executable is 50Mb or 100Mb it generally doesn’t matter - but if you add an extra 20% payload to a website, people care about that.

Should be OK, because:

- Technically speaking, if you take a single algorithm and you compile that to minified JavaScript and separately compile it to WASM, the WASM will be smaller because it’s a binary format.
- Within the web we’ve optimised for performance and size (whereas on the desktop there hasn’t been that much pressure) On the web, we have the notion of bloat, and adapted tooling: with Bootstrap, you can customise your own build, for JavaScript you can use tree shaping, which means you only deliver the required code to the browser... etc.
- You can create bloat in any technology anyways - you’ll find people putting JQuery in the page to use a single function, or all of Bootstrap when they’re only using one or two classes.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## What will happen to web frameworks?

WASMi s an efficient runtime, but it doesn’t have direct access to the DOM API and maybe never will.

Also: although it’s got the name web in it, they have been quite careful to ensure that it will work well in other execution environments.

The future of a web application might be 70-80% WASM, and the rest being JavaScript - the glue that marshals access to the DOM and CSS across its host bindings. For a native mobile application, you might have the same 70-80% WASM, but a different host binding system for the mobile device.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## What will web look like five years from now?

- we’ll still be using the browser, because it’s a fantastic distribution mechanism. Think of how email changed!! The web and browsers aren’t going away.
- But: JavaScript might lose its monopoly, and I do see people writing significant applications using a wide variety of languages on the web.
- there’s a chance that WASM will have an impact far beyond the web itself.
- We also know that on the desktop, the number of applications that are being written specifically for the desktop are diminishing over time. Add WASM to the mix, and you can start distributing applications that do heavy lifting, like CAD applications or PhotoShop.
- a certain class of application that we still struggle to distribute as a web application today will be possible.
- see it not only having an impact on the web, but also on desktop and mobile as well.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly
