--- 
layout: page
title : Publications 
permalink: /publications/
customjs:
 - sorter.js
subtitle:
banner-img: "publications_cut_scale.JPG"
---
<head>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
</head>

{% assign publications=site.data.publications | sort: 'year' | reverse %}

{% assign years=""| split: "," %}

{% for pub in publications %}
{% assign years=years | push:pub.year %}
{% endfor %}

{% assign years=years|uniq %}

{% assign preprints="false" %}
{% for paper in site.data.publications %}
    {% if paper.preprint=="true" %}
        {% assign preprints="true" %}
    {% endif %}
{% endfor %}

{% if preprints=="true" %}
<h3 class="publications-h">Preprints</h3>
<table class="publications">
{% for paper in site.data.publications %}
{% if paper.preprint=="true" %}
	<tr><td width="100%"> <a class="paperlink" target="_blank" href="{{paper.link}}"><b>{{paper.title}}</b> {% if paper.link %}<i class="fa fa-file-pdf-o"></i>{% endif %}<br>{{paper.author}} <br> {{paper.journal}}, {{paper.year}}</a></td><td></td></tr>
{% endif %}
{% endfor %}
</table>
{% endif %}

{% for i in years %}
<h3 class="publications-h">{{i}}</h3>
<table class="publications">
{% for paper in site.data.publications %}
{% unless paper.preprint=="true" %}
{% if paper.year==i %}
	<tr><td width="100%"> <a class="paperlink" target="_blank" href="{{paper.link}}"><b>{{paper.title}}</b> {% if paper.link %}<i class="fa fa-file-pdf-o"></i>{% endif %}<br>{{paper.author}} <br> {{paper.journal}}</a></td><td></td></tr>
{% endif %}
{% endunless %}
{% endfor %}
</table>
{% endfor %}

