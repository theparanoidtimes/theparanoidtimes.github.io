---
layout: page
title: ClojureScript compiler contribution
category: projects

project-repo: https://github.com/28/openlayers-cljs-compile-error-repo
ims-url: https://github.com/28/imstransport-web-site
clojurians-url: http://clojurians.net/
script-jira-url: https://clojure.atlassian.net/browse/CLJS-2004
---

I was developing a Clojure/ClojureScript Web site on Windows when I noticed this
bug. In short, the compiler produced output paths for Google Closure
dependencies that were not compatible with Windows so the builds could not pass.

I find it useful to create a entire project devoted to presenting, analyzing and
fixing the problem. So for more info about the fix see the GitHub [repo]({{ page.project-repo }}).

Thanks David Nolen and the rest of the good ClojureScript community members
over on [Clojurians slack channel]({{ page.clojurians-url }}) for helping me land this
contribution.

If you are interested in on what site I was working on, you can check it out [here]({{ page.ims-url }}).

[Update 06.04.2021.] When I was working on this I've added one more [jira]({{ page.script-jira-url }})
that will probably never be merged. Adding it here just for reference.
