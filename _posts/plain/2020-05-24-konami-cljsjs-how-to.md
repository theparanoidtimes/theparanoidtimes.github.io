---
layout: post
title: How to use the konami-js library in a ClojureScript project
category: blog

contribution-url: /contributions/2020/05/24/konami-cljsjs/
project-repo-url: https://github.com/28/konami-cljs-test
---

Recently, konami-js library [got included]({{ page.contribution-url }})
in the CLJSJS project. This post will show how to include and use the
konami-js library in your ClojureScript project.

Since all packages from CLJSJS are pushed to Clojars we can include
the konami library as a regular CLJS dependency.
This is the `:dependency` key Leiningen from `project.clj` file:
``` clojure
  :dependencies [[org.clojure/clojure "1.10.0"]
                 [org.clojure/clojurescript "1.10.520"]
                 [cljsjs/konami "1.6.2-0"]] ;; this is current version of the library
```

The library exposes only one variable which is an easter egg constructor.
It accepts only one parameter, a function that will be called when
the Konami code is inputted. The function represent the easter egg itself
and it can do whatever is needed.

Hello world example is to display a message:

``` clojure
(ns konami-cljs.core
    (:require cljsjs.konami))

(def easter-egg (js/Konami. (fn [] (js/alert "Hello Konami code!"))))
```

As mentioned the argument function can do anything. For example it
can redirect you to a different (secret) page:

``` clojure
(def easter-egg (js/Konami. (fn [] (js/window.open "https://example.com"))))
```

Once defined the `easter-egg` var can remain untouched.

Happy easter egg planting!
