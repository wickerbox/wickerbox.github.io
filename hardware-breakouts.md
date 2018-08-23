---
layout: hardware
title: Breakout Boards
permalink: /hardware/breakout-boards/
bannerimg: /img/hardware.png
---

{% for post in site.breakout-boards reversed %}

<div class="blogthumb">
  <a href="{{post.url}}"><img src="{{ post.image }}"></a>
  <div class="blogthumb-link"><a href="{{post.url}}">{{ post.title }}</a></div>
</div>

{% endfor %}

