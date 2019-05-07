--- 
layout: page
title : Research 
permalink: /research2/
banner-img: "jobs_cut_scale.JPG"
---
<h2><u>Current Projects</u></h2>
<ul>
  {% for project in site.research %}
      {% assign authors=project.authors %}
      {% assign display_current='false' %}
      {% for author in authors %}
          {% for member in site.members %}
              {% if author==member.title %}
                  {% unless member.position=='Alumni' %}
                      {% assign display_current='true' %}
                  {% endunless %}
              {% endif %}
          {% endfor %}
      {% endfor %}
      {% if display_current=='true' %}
      <li>
      <a href="{{site.baseurl}}/{{project.permalink}}">{{project.title}}</a>
      {% assign i=0 %}
      {% for author in authors %}
          {% for member in site.members %}
              {% if author==member.title %}
                  {% assign url=member.permalink %}
              {% endif %}
          {% endfor %}
          {% unless i==0 %}<span style="color: DarkGray;"> ,</span>{% endunless %}
          <a href="{{site.baseurl}}{{url}}" class="author authorlink" id="{{author}}_lnk">{{author}}</a>
          {% assign i=i | plus: 1 %}
      {% endfor %}
  </li>
  {% endif %}
  {% endfor %}
</ul>  
<h2><u>Past Projects</u></h2>
<ul>
  {% for project in site.research %}
      {% assign authors=project.authors %}
      {% assign display_current='false' %}
      {% for author in authors %}
          {% for member in site.members %}
              {% if author==member.title %}
                  {% unless member.position=='Alumni' %}
                      {% assign display_current='true' %}
                  {% endunless %}
              {% endif %}
          {% endfor %}
      {% endfor %}
      {% if display_current=='false' %}
      <li>
      <a href="{{site.baseurl}}/{{project.permalink}}">{{project.title}}</a>
      {% assign i=0 %}
      {% for author in authors %}
          {% for member in site.members %}
              {% if author==member.title %}
                  {% assign url=member.permalink %}
              {% endif %}
          {% endfor %}
          {% unless i==0 %}<span style="color: DarkGray;"> ,</span>{% endunless %}
          <a href="{{site.baseurl}}{{url}}" class="author authorlink" id="{{author}}_lnk">{{author}}</a>
          {% assign i=i | plus: 1 %}
      {% endfor %}
  </li>
  {% endif %}
  {% endfor %}
</ul>  
