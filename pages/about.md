---
layout: page
title: About
description: 零碎的思考
keywords: Petter Ma, Seventheluck
comments: true
menu: 关于
permalink: /about/
---

Open Find Get Own

Hello every buddy. :+1:


I have been working in Bank of China Software Center since graduation from university in July 2012. 
At first, I was arranged to provide prompt and efficient services on financial products purchasing in online banking for clients, 
which covered fields in demand analysis, project design and product development. Soon, out of the excellent performance of my work, 
I was promoted to be the development manager who led a team with nearly ten members. 
In the following three years, our team got gratifying achievements. 
We completed the transformation and upgrading of E-bank system for over thirty branches in Asian-Pacific and European region. 
Many influential items, such as the cash management of GE Group and Bosch Global in China and cross-border cash management of China 
Southern Airlines, Sinopec Group and Volvo Cars were handed over to our team. 

I joined in Goinvest Fund as a partner in August 2017. 
I was mainly responsible for the demand analysis, project design, and development of financial instruments and products. 
I mainly use Python, Java, and MySQL at work.


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
