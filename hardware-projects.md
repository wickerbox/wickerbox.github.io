---
layout: hardware
title: Projects
permalink: /hardware/projects/
bannerimg: /img/hardware.png
---

<div class="flex-container flex-wrap">
  {% for post in site.projects reversed %}
  <div class="webthumb">
    <a href="{{post.url}}"><img src="{{ post.image }}"></a>
    <div class="webthumb-link"><a href="{{post.url}}">{{ post.title }}</a></div>
  </div>
  {% endfor %}
</div>
