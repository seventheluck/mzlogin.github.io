---
layout: page
title: About
description: Petter Ma
keywords: Petter Ma, Seventheluck
comments: true
menu: 关于
permalink: /about/
---

Open Find Get Own

Hello every buddy. :+1:


:+1:+1:+1:+1:+1


## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
