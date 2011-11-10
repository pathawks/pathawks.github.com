---
title: Open Graph data in Blogger
layout: post
---
Adding [Open Graph metadata](http://ogp.me/) to a website can be a pain, and will almost certainly break your validation unless you're using an RDFa Doctype…

Who am I kidding? Nobody ever uses RDFa Doctypes.

Fortunately for [Blogger](http://blogger.com) users, Blogger blogs never validate anyway, so adding Open Graph metadata is easy.

Simply copy the code below and paste it into your template after the `<header>` tag.
<script src="https://gist.github.com/1343315.js">
</script><noscript><code><pre>
<!-- Begin Open Graph metadata -->
<b:if cond='data:blog.pageType == &quot;item&quot;'>
	<meta content='article' property='og:type'/>
	<meta expr:content='data:blog.title' property='og:site_name'/>
	<meta expr:content='data:blog.pageName' property='og:title'/>
	<b:if cond='data:blog.postImageThumbnailUrl'>
		<meta expr:content='data:blog.postImageThumbnailUrl' property='og:image'/>
	</b:if>
<b:else/>
	<meta expr:content='data:blog.title' property='og:title'/>
	<meta content='website' property='og:type'/>
</b:if>
<meta expr:content='&quot;en_US&quot;' property='og:locale'/>
<meta expr:content='data:blog.canonicalUrl' property='og:url'/>
<!-- End Open Graph metadata -->
</code><pre></noscript>

I've added this code to [a Gist](https://gist.github.com/1343315), so feel free to fork it and modify it as you see fit. If you do something really cool, I'd love to hear about it.

A couple notes:

*   `og:locale` Should probably actually reflect the blog's locale instead of just being  a hardcoded string. Unfortunately, Blogger only gives us `en-us` with a hyphen, instead of an underscore, so that won't work.

*   If you're using your blog as a personal profile, you may consider changing the second `og:type` from `website` to `profile` and adding [your personal information](http://ogp.me/#type_profile)

*   `og:image` Is only supplied if Blogger finds an image in the current post. However, not supplying `og:image` is invalid. You could provide an alternate image to provide in these circumstances, perhaps your Gravatar or blog's logo.