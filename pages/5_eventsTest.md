--- 
layout: page
title : Events2 
permalink: /events2/
banner-img: "events_cut_scale.JPG"
---
{% capture this_year %}{{'now' | date: '%Y'}}{% endcapture %}
{% assign last_year=this_year| minus:1 %}

{% assign talks=site.talks |sort: 'date' %}

<!-- hidden table with all dates to be dsplayed on main page -->
<table id="cur_data" style="display: none;">
<thead>
    <tr><th>year</th><th>date</th><th>title</th><th>speaker</th><th>affiliation</th><th>location</th><th>content</th></tr>
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
		<td>{{talk.content|strip_html|truncate:170}}</td>
	    </tr>
	{% endif %}
    {% endfor %}
</tbody>
</table>

<div id="events">
	<h2>Past Events</h2>
</div>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script>
    var today = new Date()
		
    var first_future_talk = 0;
    $('#cur_data tbody tr').each(function(){
    var test = $(this).find('td:eq(1)').text()
    var test_date = new Date(test);
    future = test_date >= today;
    if (future == true){return false}
    first_future_talk += 1
    });
    
    var monthNames = [
    "January", "February", "March",
    "April", "May", "June", "July",
    "August", "September", "October",
    "November", "December"
    ];
    
    var year;
    var date;
    var title;
    var speaker;
    var affiliation;
    var location;
    
    var table_handle;
    
    var day;
    var mon;
    
    var table = document.getElementById("cur_data");
    var cells;
    
    var j = first_future_talk + 1;
    var year_old = 0;
    while(j < table.rows.length ){
	      cells = table.rows[j].cells;
	      year = cells[0].innerHTML;
	      dt = cells[1].innerHTML;
	      ttl = cells[2].innerHTML;
	      spkr = cells[3].innerHTML;
	      aff = cells[4].innerHTML;
	      loc = cells[5].innerHTML;
	      con = cells[6].innerHTML;
	      
	      dt_obj = new Date(dt);
	      day = dt_obj.getDate();
  	      mon = monthNames[dt_obj.getMonth()];
	      
	      if (year > year_old){
	          table_handle = 'future_'+year;
	          $('#events').append("<h3>"+year+"</h3>");
                  $('#events').append("<table id='"+table_handle+"' class='talks' style='overflow: hidden;'></table>");
	          year_old = year;
	      }
	      $('#'+table_handle).append("<tr><td><b>"+spkr+"</b><span class='affil'> ["+aff+"] </span><span class='event_date'>"+day+" "+mon+", "+year+"</span><br><i>"+ttl+"</i><br><div id='abstractbox'>"+con+"</div></td></tr>");
	      j += 1;
	  }
    
    j = first_future_talk;
    year_old = table.rows[j].cells[0].innerHTML + 1;
    
    while(j >= 1){
	      cells = table.rows[j].cells;
	      year = cells[0].innerHTML;
	      dt = cells[1].innerHTML;
	      ttl = cells[2].innerHTML;
	      spkr = cells[3].innerHTML;
	      aff = cells[4].innerHTML;
	      loc = cells[5].innerHTML;
	      con = cells[6].innerHTML;
	      
	      dt_obj = new Date(dt);
	      day = dt_obj.getDate();
  	      mon = monthNames[dt_obj.getMonth()];
	      
	      if (year < year_old){
	          table_handle = 'past_'+year;
	          $('#events').append("<h3>"+year+"</h3>");
                  $('#events').append("<table id='"+table_handle+"' class='talks' style='overflow: hidden;'></table>");
	          year_old = year;
	      }
	      $('#'+table_handle).append("<tr><td><b>"+spkr+"</b><span class='affil'> ["+aff+"] </span><span class='event_date'>"+day+" "+mon+", "+year+"</span><br><i>"+ttl+"</i><br><div id='abstractbox'>"+con+"</div></td></tr>");
	      j -= 1;
	  }
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
