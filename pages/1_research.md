--- 
layout: page
title : Research 
permalink: /research/
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
      {% if project.force_past_projects!='true' and display_current=='true' or project.force_current_projects=='true' %}
      <li>
      <a href="{{site.baseurl}}/{{project.permalink}}">{{project.title}}</a>
      {% assign i=0 %}
      {% for author in authors %}
	  {% assign is_mkp='false' %}
          {% for member in site.members %}
              {% if author==member.title %}
	          {% assign is_mkp='true' %}
                  {% assign position=member.position %}
                  {% if position !='Alumni' %}
                      {% assign url=member.permalink %}
				          {% else %}
				              {% assign url='/team/#alumni' %}
				        {% endif %}
              {% endif %}
          {% endfor %}
          {% unless i==0 %}<span style="color: DarkGray;"> ,</span>{% endunless %}
         <a href="{% if site.data.external_researchers[author] %}{{site.data.external_researchers[author]}}{% elsif is_mkp=='true' %}{{site.baseurl}}{{url}}{% else %}javascript:;{% endif %}" class="author authorlink {%unless is_mkp=='true' or site.data.external_researchers[author] %}inactive{% endunless %}" id="{{author}}_lnk">{{author}}</a>
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
      {% if project.force_past_projects=='true' or display_current=='false' and project.force_current_projects!='true' %}
      <li>
      <a href="{{site.baseurl}}/{{project.permalink}}">{{project.title}}</a>
      {% assign i=0 %}
      {% for author in authors %}
          {% for member in site.members %}
              {% if author==member.title %}
                  {% assign position=member.position %}
                  {% if position !='Alumni' %}
                       {% assign url=member.permalink %}
				          {% else %}
				            {% assign url='/team/#alumni' %}
				        {% endif %}
              {% endif %}
          {% endfor %}
          {% unless i==0 %}<span style="color: DarkGray;"> ,</span>{% endunless %}
          <a href="{% if site.data.external_researchers[author] %}{{site.data.external_researchers[author]}}{% elsif is_mkp=='true' %}{{site.baseurl}}{{url}}{% else %}javascript:;{% endif %}" class="author authorlink {%unless is_mkp=='true' or site.data.external_researchers[author] %}inactive{% endunless %}" id="{{author}}_lnk">{{author}}</a>
          {% assign i=i | plus: 1 %}
      {% endfor %}
  </li>
  {% endif %}
  {% endfor %}
</ul>  
