---
layout: post
title: City Street Orientations Serbia
category: blog
gboeing-blog-url: https://geoffboeing.com/2018/07/comparing-city-street-orientations/
osmnx-install-url: https://geoffboeing.com/2016/11/osmnx-python-street-networks/
osmnx-repo: https://github.com/gboeing/osmnx
osmnx-example-repo: https://github.com/gboeing/osmnx-examples
osmnx-script-repo: https://github.com/28/osmnx-city-street-network-orientations
street-orientations-example-repo: https://github.com/gboeing/osmnx-examples/blob/master/notebooks/17-street-network-orientations.ipynb
gboeing-t: https://twitter.com/gboeing
belgrade-map: https://www.openstreetmap.org/#map=12/44.8084/20.5146
---

When I saw this amazing blog [post]({{ page.gboeing-blog-url }}) by [Geoff Boeing]({{ page.gboeing-t }})
I immediately wanted to do the same thing for some cities of my choice (and to
play with the great tool that is [*osmnx*]({{ page.osmnx-repo }})). I strongly
suggest reading the mentioned blog (and the follow up one mentioned there) before going
further.

Setting up the environment is easy - this [post]({{ page.osmnx-install-url }})
describes how to install and use *osmnx* and there are a lot of examples in the form of
*Jupyter* notebooks [here]({{ page.osmnx-example-repo }}). [This]({{ page.street-orientations-example-repo }})
particular one was used to create the city street orientations images, although I
used a script because I found it easier. You can see the script [here]({{ page.osmnx-script-repo }})<sup id="f1r">[1](#f1)</sup>.

So, naturally, my home town came first.

[Belgrade]({{ page.belgrade-map }}), Serbia:

![Belgrade streets](/public/img/street/belgrade.png "Belgrade streets")

After that I decided to get the street orientations for all major cities in Serbia.
Since there are a lot of cities I divided them into a couple of groups<sup id="f2r">[2](#f2)</sup>.

Here they are...

Vojvodina:

![Vojvodina cities streets](/public/img/street/vojvodina_s.png "Vojvodina cities streets")

Central Serbia:

![Central Serbia cities streets](/public/img/street/central_s.png "Central Serbia cities streets")

South Serbia:

![South Serbia cities streets](/public/img/street/south_s.png "South Serbia cities streets")

Novi Pazar region:

![Novi Pazar region cities streets](/public/img/street/np_s.png "Novi Pazar region cities streets")

And Kosovo:

![Kosovo cities streets](/public/img/street/kosovo_s.png "Kosovo cities streets")

### Conclusion ###

Serbia is a land with a really unique geography and really unique sequence of
events that happened throughout its history. Various geopolitical moments had
impact on all aspects of human living and doing in the region, one of them being
the way cities were built. Layout of the city streets is different for almost
every city which can be seen by the pictures in this post. I'm certain that
it is possible to find a connection between people who lived there, geographical,
historical or political moments and the particular 'shape' that one city has.
To me this is a very interesting topic for a research.

I'm not trying to be the 'here is the data, I'm done, now someone do the
research' guy, but at the first glance, there are not many resources online that
tackle the question of urbanism in Serbia so it is really hard to find any data
to run this images by. Certainly there are books in the archives somewhere that
can be used in such a research, but just finding them can be a very time consuming
effort.

I will have my eyes open for anything related and I will try to post anything
that I can find here. Meanwhile, I hope that someone gets inspired to conduct
any kind of research (or they already did). One thing is certain - [*osmnx*]({{ page.osmnx-repo }})
is the tool for the job.

Thanks to [Geoff Boeing]({{ page.gboeing-t }}) for the inspiration. :-)

Any discussion is welcome on [Twitter]({{ site.twitter-url }}).

*Fin*

---
{% include footnote.html n=1 nid="f1" text="You may notice that for some cities I had to
query for 'municipality' because towns were not available on their own. Municipalities
include a wider region than the city so this could have had impact on the end results." r="#f1r" %}
{% include footnote.html n=2 nid="f2" text="Division was not based on any political,
religious or ethnic criteria, I just found it easier to do it this way." r="#f2r" %}
