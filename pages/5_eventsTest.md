--- 
layout: page
title : Events2 
permalink: /events2/
banner-img: "events_cut_scale.JPG"
---
{% capture this_year %}{{'now' | date: '%Y'}}{% endcapture %}
{% assign last_year=this_year| minus:1 %}

{% assign talks=site.talks |sort: 'date' %}

{% assign cur_years=""| split: "," %}

<!-- hidden table with all dates to be dsplayed on main page -->
<table id="cur_data">
<thead>
    <tr><th>year</th><th>date</th><th>title</th><th>speaker</th><th>affiliation</th><th>location</th></tr>
</thead>
<tbody>
    {% for talk in talks %}
	{% assign talk_year=talk.date|date:'%Y' %}
	{% assign talk_year=talk_year|plus:0 %}
	{% if talk_year >= last_year %}
	    <tr>
	        <td>{{talk_year}}</td>
		<td>{{talk.date}}</td>
		<td>{{talk.title}}</td>
		<td>{{talk.speaker}}</td>
		<td>{{talk.affiliation}}</td>
		<td>{{talk.location}}</td>
	    </tr>
	    {% assign cur_years=cur_years | push: talk_year %}
	{% endif %}
    {% endfor %}
</tbody>
</table>
{% assign cur_years=cur_years|uniq %}

<div id="events">
	<h2>Past Events</h2>
</div>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script>
    var current_year = (new Date).getFullYear();
    var today = new Date()
    var end_year = current_year + 10;
    var s = {{cur_years}};
    var years_con = s.toString()
    var years = new Array();
    <!--
    var i = 4;
    do {
        years.push(years_con.substring(0, i));
        } while((years_con = years_con.substring(i, years_con.length)) != "");
    -->
		
    var first_future_talk = 0;
    $('#cur_data tbody tr').each(function(){
    var test = $(this).find('td:eq(1)').text()
    var test_date = new Date(test);
    future = test_date >= today;
    if (future == true){return false}
    first_future_talk += 1
    });
    
    var j = first_future_talk - 1;
    var table = document.getElementById("cur_data");
    var cells;
    var year_old = table.rows[j].cells[0].innerHTML + 1;
    var year;
    
    var table_handle;
    
    while(j >= 1){
	      cells = table.rows[j].cells;
	      year = cells[0].innerHTML;
	      if (year < year_old){
	          table_handle = 'past_'+year;
		  alert(table_handle);
	          $('#events').append("<h3>"+year+"</h3>");
                  $('#events').append("<table id='past_"+year+"' class='talks' style='overflow: hidden;'><tr><td>test</td></tr></table>");
	          year_old = year;
	      }
	      j -= 1;
	  }
    <!--
    years.reverse().forEach(function(year) {
      if(year <= current_year){
          $('#events').append("<h3>"+year+"</h3>");
          $('#events').append("<table id='past_"+year+"' class='talks' style='overflow: hidden;'></table>");
	  var j = first_future_talk - 1;
	  
	  var table = document.getElementById("cur_data");
	  var cells;
	  while(j > 7){
	      cells = table.rows[j].cells;
	      j -= 1;
	  }
	  }
    });
    -->
</script>


{% assign talks_rev=site.talks |sort: 'date' %}
{% assign talks=talks_rev | reverse %}

{% assign years=""| split: "," %}
{% assign dates=""| split: "," %}

{% capture nowunix %}{{'now' | date: '%s'}}{% endcapture %}

{% for talk in talks %}
{% assign year=talk.date | date: "%Y" %}
{% assign years=years | push:year %}
{% assign date=talk.date | date:  '%s' %}
{% assign dates=dates | push: date %}
{% endfor %}

{% assign future_years="" | split: "," %}
{% assign past_years=""| split: "," %}
{% for date in dates %}
  {% assign year=date|date:"%Y" %}
  {% if date < nowunix %}
    {% assign past_years=past_years | push: year %}
  {% else %}
        {% assign future_years=future_years | push: year %}
  {% endif %}
{% endfor %}

{% assign years=years|uniq %}
{% assign years_rev=years|reverse %}

<!-- Future -->
<h2>Upcoming Events</h2>
{% for i in years_rev %}
{% if future_years contains i %}
<h3>{{i}}</h3>
<table class="talks" style="overflow: hidden;">
<tbody>
{% for talk in talks_rev %}

{% assign year=talk.date|date: "%Y" %}
{% capture date %}{{talk.date | date: '%s'}}{% endcapture %}

{% if date >= nowunix %}
{% if year==i %}
    {%if talk.img %}
      {% assign imgurl=talk.img %}
    {% else %}
      {% assign imgurl=site.emergency-img %}
    {%endif%}

	<tr onclick="location.href='{{ talk.url | prepend: site.baseurl }}'">
            <td><b>{{talk.speaker}}</b> <span class="affil">{%if talk.affiliation %}[{{talk.affiliation}}]{% endif %}</span><span class="event_date">{{talk.date| date: "%B %-d, %Y"}}</span><br><i>{{talk.title}}</i><br><div id="abstractbox">{{talk.content|strip_html|truncate:170}}</div></td><td></td>
        </tr>
{% endif %}
{% endif %}
{% endfor %}
</tbody>
</table>
{% endif %}
{% endfor %}

<!-- Past -->
<h2>Past Events</h2>
{% for i in years %}
{% if past_years contains i %}
<h3>{{i}}</h3>
<table class="talks" style="overflow: hidden;">
<tbody>
{% for talk in talks %}

{% assign year=talk.date|date: "%Y" %}
{% capture date %}{{talk.date | date: '%s'}}{% endcapture %}

{% if date < nowunix %}
{% if year==i %}
    {%if talk.img %}
      {% assign imgurl=talk.img %}
    {% else %}
      {% assign imgurl=site.emergency-img %}
    {%endif%}

	<tr onclick="location.href='{{ talk.url | prepend: site.baseurl }}'">
            <td><b>{{talk.speaker}}</b> <span class="affil">{% if talk.affiliation %}[{{talk.affiliation}}]{% endif %}</span><span class="event_date">{{talk.date| date: "%B %-d, %Y"}}</span><br><i>{{talk.title}}</i><br><div id="abstractbox">{{talk.content|strip_html|truncate:170}}</div></td><td></td>
        </tr>
{% endif %}
{% endif %}
{% endfor %}
</tbody>
</table>
{% endif %}
{% endfor %}
