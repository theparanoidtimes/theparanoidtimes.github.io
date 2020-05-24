---
layout: page
title: konami-js library to cljsjs project
category: contributions

konami-js-url: http://snaptortoise.github.io/konami-js/
cljsjs-url: http://cljsjs.github.io
commit-url: https://github.com/cljsjs/packages/commit/214e8c316001ace6b262829c4d4eabfb63b7bad6
konami-code-url: https://en.wikipedia.org/wiki/Konami_Code
extern-creator-url: https://jmmk.github.io/javascript-externs-generator/
npm-unpkg-url: https://unpkg.com/
build-boot-file-url: https://github.com/cljsjs/packages/blob/master/konami/build.boot
---

[konami-js]({{ page.konami-js-url }}) is a small JS library that I,
more often than not, used in various projects. The library introduces
the [Konami code]({{ page.konami-code-url }}) easter egg to your project.
Its a fun little feature  which I wanted to bring a bit closer to the ClojureScript
community so I opted in to add it to the [CLJSJS]({{ page.cljsjs-url }}) project.
CLJSJS project packages JavaScript libraries with Google Closure externs which
makes them easily accessible from ClojureScript projects. You can access all
libraries packaged this way as a simple ClojureScript dependency.

There is a great tutorial on CLJSJS GitHub page wiki on how to contribute
to the project and the whole process is fairly easy. Two most important
things are creating a `build.boot` and an externs file. There is a
pretty much standard way for doing them both which utilizes external 
services. Primary thing in the `build.boot` file is to define the location
of the JavaScript library source. A lot of libraries use the [unpkg.com]({{ page.npm-unpkg-url }})
service if the source library is hosted on npm which konami-js is. The rest
of the file is a standard way to pack a library. See the file [here]({{ page.build-boot-file-url }}).
The externs file is needed for the ClojureScript advanced compilation.
There are tools online for creating an externs file such as [javascript-externs-generator]({{ page.extern-creator-url }}).

The pull request was merged in main with this [commit]({{ page.commit-url }}).
