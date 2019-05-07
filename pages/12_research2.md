--- 
layout: page
title : Research 
permalink: /research2/
banner-img: "jobs_cut_scale.JPG"
---
<h2><u>Current Projects</u></h2>
<ul>
  {% for project in site.research %}
  <li><a href="{{site.baseurl}}/{{project.permalink}}">{{project.title}}</a></li>
  {% endfor %}
</ul>  
<h2><u>Past Projects</u></h2>
