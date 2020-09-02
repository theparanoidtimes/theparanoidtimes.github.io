---
layout: page
title: The Warriors movie tribute
category: projects
permalink: /:categories/:title

repo-url: https://github.com/28/thewarriors-path
project-url: https://28.github.io/thewarriors-path/
open-layers-url: https://openlayers.org
---

_The Warriors_ movie is one of my favorites and after seeing it for
the millionth time I wanted to visualize the path the gang took on a map.
The story is set in a fictional future in New York city so naturally,
I could not count on that the train network is the same as in modern
New York. The goal is to project the path on the modern New York
network as accurately as possible. The task proved to be much easier
than I thought. The whole story is based on the gang moving through
the city via the 'optimal' path (where optimal here means not getting
killed) so evidence of their whereabouts is presented everywhere - the
dialog, shooting locations, landmarks, etc. I just needed to collect
them all. Since I wanted to present the path the story describes and
not the map of the shooting locations the primary source of truth was
the dialog because shooting locations and the story locations often
don't match. It is because of this that for some parts I had to use
my free interpretation.

See the site [here]({{ page.project-url }}).

The application is written in ClojureScript and uses [OpenLayers]({{ page.open-layers-url }}) to 
display the map and the path. The data is stored in the _edn_ file
which is organized by movie segments (from Van Cortland to Tremont,
train station - Baseball Furies, etc). Each movie segment is displayed
as a separate path on the map using a different color. The code follows
the vector of geographical points and draws them on the map alongside
drawing the path line between them. Special points in the file marked
with `:story` type have story text attached to them which can be
viewed in the popup window when clicked on them. You can see the
source code [here]({{ page.repo-url }}).

I think it does a fairly nice job of presenting the story that is 
told in the movie and it was really fun making it.

I hope you enjoy it as much as I had fun making it.
