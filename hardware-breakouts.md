---
layout: hardware
title: Breakout Boards
permalink: /hardware/breakout-boards/
bannerimg: /img/hardware.png
---

<div class="flex-container flex-wrap">
  {% for post in site.breakout-boards reversed %}
  <div class="webthumb">
    <a href="{{post.url}}"><img src="{{ post.image }}"></a>
    <div class="webthumb-link"><a href="{{post.url}}">{{ post.title }}</a></div>
  </div>
  {% endfor %}
</div>
