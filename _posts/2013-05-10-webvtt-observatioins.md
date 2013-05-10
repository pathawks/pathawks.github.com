--- 
layout: "post"  
date: "2013-05-10 19:15:00-4:00"  
author:  
    name: "Pat Hawks"  
    url: "http://pathawks.com"
title: "WebVTT Observations"  
---

According to the [WebVTT Draft Spec](http://dev.w3.org/html5/webvtt/#dfn-webvtt-file-body), a WebVTT file must start with the string "WEBVTT" followed by some text that **does not** include a line break, followed by two line breaks. This pretty much kills the idea of including header metadata. Yet, WebVTT files produced by YouTube break this rule and include some extra data in the header (along with line breaks), breaking the spec.

{% highlight text %}
WEBVTT
Kind: captions
Language: en
  
  
{% endhighlight %}

It would be nice if the spec allowed for metadata to be added like this. It would be nice if the spec allowed for something like RDF or microdata, but I understand that one of the beauties of WebVTT is its low _markup to content_ ratio.

Additionally, it would be nice to have support for a GUID, or even an alternative content link to the webpage where this WebVTT file is embedded, or even a link directly to the video file this WebVTT file belongs with. This way, if the WebVTT file is orphaned, one can make a reasonable guess about what it is and where it belongs without the contextual data from the parent HTML document.

It would be nice to have a semantic way to markup sounds, or even who is speaking. Currently, we can use [voice tags](http://dev.w3.org/html5/webvtt/#dfn-webvtt-cue-voice-span), but that only seems to get us part of the way there. Note: I'm thinking about this mostly from a "Search Engines Indexing Captions" perspective.

Why doesn't the HTML `<track>` element support the `type` attribute, like the `<source>` element? What happens when we discover the thing that is way better than WebVTT? This seems like a step in the wrong direction.

WebVTT files **must** be UTF-8. The `Content-Type` must be [`text/vtt`](http://dev.w3.org/html5/webvtt/#text-vtt), and specifies no required or optional parameters. Why, then, are so many WebVTT files being served with the Content-Type `text/vtt; charset=utf-8`?

If [WebVTT cue identifiers can contain spaces](http://dev.w3.org/html5/webvtt/#dfn-webvtt-cue-identifier), how would we reference these IDs in CSS?
