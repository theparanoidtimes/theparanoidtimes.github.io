---
layout: post
title: Hidden in plain Java
category: blog
filer-url: /projects/filer
filer-repo: https://github.com/theparanoidtimes/filer
java-test-file-url: https://github.com/theparanoidtimes/filer/blob/master/java/FilerMain.java
---

Today we are able to receive dozens of e-mail messages in our mailbox daily.
Most of them are related to some marketing campaign, TC updates, promotions etc.
that we take for granted and in most cases they all get deleted. However, all
these are the result of a huge effort from marketing and development teams that
work together to produce layouts that are great looking and that efficiently
convey the message to the end user.

In my company we are developing and maintaining an in-house mass mailing system
that at peak performance can send around 200k messages in an hour. To our client,
and probably for anyone, it is extremely important that each of the sent
messages looks and behaves exactly as it should. This is why we invest a lot of
time in testing the end look of each message type we send.

We have developed a lot of tools to help the cause, but they all come down to
comparing the produced message with the expected output. In case of plain text
message part<sup id="f1r">[1](#f1)</sup> we compare the whole text with the
expected one including every whitespace character. And in case of HTML part we
semantically compare the whole output - basically ignore whitespace outside the
tags. Comparing the whole output word by word can prove to be a huge overhead
when doing it for a couple of dozens of message types. Almost 90% of the message
content is the same across types so effectively one can test that 90% once and
for each message type test only that is specific for it - the remaining 10%.
This is where the idea for the [*filer*]({{ page.filer-url }}) came up. To pick
critical parts of each message type and assert its validity instead of checking
the whole thing again and again. Check out the [project page]({{ page.filer-url }})
for more info on how can this be achieved with the help of this
library<sup id="f2r">[2](#f2)</sup>.

However, when I tried to introduce this library to my colleagues there was a
slight rejection. Although the whole team is made of Java programmers none was
familiar with Clojure. So in order to bring the language a bit closer to them
and hopefully motive them to start learning it I decided to, as some kind of
challenge, create a project that will provede a seamless transition from Java to
Clojure.

Using the Clojure Java interop functionality and the fact that Clojure is a
hosted language I decided to 'hide' the library in a jar and provide a Java
interface for using it.

The interface should not be overwhelming and should be easy to use. *filer* makes
this easier as it provides some helper functions that are useful for common tasks
like assert on link target or node content and similar. To make things less
complicated I wrote wrapper functions around the *filer* core functionalities in
a separate namespace<sup id="f3r">[3](#f3)</sup> and the next thing was to expose
them:

``` clojure
(gen-interface
  :name "org.theparanoidtimes.filer.html.assertion.NodeAssertionInstruction")

(gen-interface
  :name "org.theparanoidtimes.filer.html.assertion.NodeContentAssertionInstruction"
  :extends [org.theparanoidtimes.filer.html.assertion.NodeAssertionInstruction]
  :methods [[assertOnContent [String] Boolean]])

(gen-class
  :name "org.theparanoidtimes.filer.html.assertion.HtmlAssertion"
  :prefix "java-"
  :methods [^:static [assertNodeContentIsEqual [Object String String] Boolean]
            ^:static [assertNthNodeContentIsEqual [Object String String Integer] Boolean]
            ^:static [assertNodeContentMatches [Object String java.util.regex.Pattern] Boolean]
            ^:static [assertNodeAttributeValue [Object String String String] Boolean]
            ^:static [assertLinkNameIsEqual [Object String String] Boolean]
            ^:static [assertLinkTargetIsEqual [Object String String] Boolean]
            ^:static [assertImageSrcIsEqual [Object String String] Boolean]
            ^:static [assertImageSrcAndAltAreEqual [Object String String String] Boolean]
            ^:static [assertImageAsLinkIsEqual [Object String String String] Boolean]
            ^:static [assertOnNodeContent [Object String org.theparanoidtimes.filer.html.assertion.NodeContentAssertionInstruction]
```

The code above exposes the wrapper functions as static methods and introduces
two interfaces which I will explain later. In order for this to work the namespace
in question should be *aot* compiled, so the following line was added to `project.clj`:
```clojure
:aot [org.theparanoidtimes.filer.html.assertion]
```

With everything set and library added as a dependency in a Java project we can
finally do this:

```java
import static org.theparanoidtimes.filer.html.assertion.HtmlAssertion.*;
...
File testHtml = new File("test.html");
Boolean result = HtmlAssertion.assertNodeContentIsEqual(testHtml, "div#top > header > h1", "HTML5 Test Page");

result = assertLinkTargetIsEqual(testHtml, "article#embedded__progress > footer > p > a", "#top");
```

Translated into Clojure it looks like this:
```clojure
(assert-select test-html [:div#top :> :header :> :h1] (content=? "HTML5 Test Page"))

(assert-select test-html [:article#embedded__progress :> :footer :> :p :> :a] (link-target=? "#top"))
```

Note that the node path in the Java code is a plain String without colons in words.
This feels more natural in Java code and conversion is done by the *filer* wrapper
functions. These examples are run against the HTML test file in the
[*filer* repo]({{ page.filer-repo }}). For more Java examples check out
[this]({{ page.java-test-file-url }}) file.

Two interfaces are introduced also. The idea is by using them we can perform custom
assertions on various parts of the HTML file. The first interface is
`NodeAssertionInstruction` that has no methods and it is just a parent interface
for all others. Currently it has one child - `NodeContentAssertionInstruction`
which exposes a method for doing custom assertions on particular node's content.

So, for example, this Clojure code that checks if all `li` items have any content:
```clojure
(assert-select test-html [:li] (complement (content=? ""))
```
becomes this Java code:
```java
Boolean result = assertOnNodeContent(testHtml, "li", content -> !content.equals(""));
```

With Java's lambda expressions it is really easy to transition to Clojure functional
point of view. Also there is a slight similarity in the looks in both invocations.
More interfaces can be introduced in order to cover all functionalities of *filer*.
But that is not the point of this experiment and it is also not practical. The
point was to bring Clojure closer to the user via plain Java.

Having this kind of Java library is not practical simply because it is not
maintainable in any way. In order to add some new functionality or change the
existing, one must do so in multiple layers in Clojure and recompile the library
to use it in Java code. Also, if anything goes wrong the error messages are
completely incomprehensible and it is almost impossible to debug. So this kind
of exhibitions should be left only for exercise and fun.

In my particular case this approach proved effective since it sparked an interest
in Clojure with my colleagues. It is always good to introduce new technologies
into the programming collective since it can spark new ideas and renew the motivation
in people. It is also good to be creative in doing so since it brings fun to
learning. I hope this little experiment proves that statement.

---
{% include footnote.html n=1 nid="f1" text="We send multipart e-mail messages always even
though only a small percent of e-mail clients can't read HTML messages." r="#f1r" %}
{% include footnote.html n=2 nid="f2" text="The focus is on the HTML assertion part
of the library as it has functionalities regarding directories, plain text files and
XML files." r="#f2r" %}
{% include footnote.html n=3 nid="f3" text="org.theparanoidtimes.filer.html.assertion
namespace in the repo." r="#f3r" %}
