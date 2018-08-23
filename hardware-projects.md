---
layout: hardware
title: Projects
permalink: /hardware/projects/
bannerimg: /img/hardware.png
---

{% for post in site.projects reversed %}

<div class="blogthumb">
  <a href="{{post.url}}"><img src="{{ post.image }}"></a>
  <div class="blogthumb-link"><a href="{{post.url}}">{{ post.title }}</a></div>
</div>

{% endfor %}

