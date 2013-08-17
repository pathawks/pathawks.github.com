--- 
layout: "post"  
date: "2013-05-10 19:15:00-4:00"  
permalink: "/webvtt-observatioins.html"  
guid: "http://alt.pathawks.com/webvtt-observatioins"  
title: "WebVTT Observations"  
---

**UPDATE: See clarification from WebVTT at the bottom of this post.**

According to the [WebVTT Draft Spec](http://dev.w3.org/html5/webvtt/#dfn-webvtt-file-body), a WebVTT file must start with the string "WEBVTT" followed by some text that **does not** include a line break, followed by two line breaks. This pretty much kills the idea of including header metadata. Yet, WebVTT files produced by YouTube break this rule and include some extra data in the header (along with line breaks), breaking the spec.

{% highlight text %}
WEBVTT
Kind: captions
Language: en
  
  
{% endhighlight %}

It would be nice if the spec allowed for metadata to be added like this. It would be nice if the spec allowed for something like RDF or microdata, but I understand that one of the beauties of WebVTT is its low _markup to content_ ratio.

Additionally, it would be nice to have support for a GUID, or even an alternative content link to the webpage where this WebVTT file is embedded, or even a link directly to the video file this WebVTT file belongs with. This way, if the WebVTT file is orphaned, one can make a reasonable guess about what it is and where it belongs without the contextual data from the parent HTML document.

It would be nice to have a semantic way to markup sounds, or even who is speaking. Currently, we can use [voice tags](http://dev.w3.org/html5/webvtt/#dfn-webvtt-cue-voice-span), but that only seems to get us part of the way there. Note: I'm thinking about this mostly from a "Search Engines Indexing Captions" perspective.

On that note, when will we be able to include WebVTT files in Video Sitemaps?

Why doesn't the HTML `<track>` element support the `type` attribute, like the `<source>` element? What happens when we discover the thing that is way better than WebVTT? This seems like a step in the wrong direction.

WebVTT files **must** be UTF-8. The `Content-Type` must be [`text/vtt`](http://dev.w3.org/html5/webvtt/#text-vtt), and specifies no required or optional parameters. Why, then, are so many WebVTT files being served with the Content-Type `text/vtt; charset=utf-8`?

If [WebVTT cue identifiers can contain spaces](http://dev.w3.org/html5/webvtt/#dfn-webvtt-cue-identifier), how would we reference these IDs in CSS?

---

The folks at WebVTT contacted me on Twitter regarding metadata at the begining of the file.  
I believe the bug referred to is [Bug 15851](https://www.w3.org/Bugs/Public/show_bug.cgi?id=15851).

{% raw %}
<blockquote class="twitter-tweet"><p><a href="https://twitter.com/PatHawks">@pathawks</a> Actually, it&#39;s not disallowed - it&#39;s just not part of the syntax spec. The parsing spec, however, parses it out.</p>&mdash; webvtt (@webvtt) <a href="https://twitter.com/webvtt/statuses/346206768357076992">June 16, 2013</a></blockquote>
<blockquote class="twitter-tweet" data-conversation="none"><p><a href="https://twitter.com/webvtt">@webvtt</a> &quot;…followed by any number of characters that are not LINE FEED (LF) or CARRIAGE RETURN (CR) characters&quot; <a href="http://t.co/MKBd3tyh9t">http://t.co/MKBd3tyh9t</a></p>&mdash; Pat Hawks (@PatHawks) <a href="https://twitter.com/PatHawks/statuses/346408488207015936">June 16, 2013</a></blockquote>
<blockquote class="twitter-tweet" data-conversation="none"><p><a href="https://twitter.com/PatHawks">@pathawks</a> right, but then it needs 2 line terminators to move on, so single newlines are also ignored</p>&mdash; webvtt (@webvtt) <a href="https://twitter.com/webvtt/statuses/346440001107656704">June 17, 2013</a></blockquote>
<blockquote class="twitter-tweet" data-conversation="none"><p><a href="https://twitter.com/webvtt">@webvtt</a> Understood. It just seems like the spec could mention this use case. Is there a reason to leave it out?</p>&mdash; Pat Hawks (@PatHawks) <a href="https://twitter.com/PatHawks/statuses/346457637220655104">June 17, 2013</a></blockquote>
<blockquote class="twitter-tweet" data-conversation="none"><p><a href="https://twitter.com/PatHawks">@pathawks</a> the editor hasn&#39;t got around to it yet - there&#39;s a bug in the bug tracker :-)</p>&mdash; webvtt (@webvtt) <a href="https://twitter.com/webvtt/statuses/346461911677808640">June 17, 2013</a></blockquote>
<blockquote class="twitter-tweet" data-conversation="none"><p><a href="https://twitter.com/webvtt">@webvtt</a> I’m glad to hear it :)</p>&mdash; Pat Hawks (@PatHawks) <a href="https://twitter.com/PatHawks/statuses/346487938168811520">June 17, 2013</a></blockquote>
{% endraw %}
