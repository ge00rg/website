--- 
layout: page
title : Events 
permalink: /events/
banner-img: "events_cut_scale.JPG"
---
{% capture this_year %}{{'now' | date: '%Y'}}{% endcapture %}
{% assign last_year=this_year| minus:1 %}

{% assign talks=site.talks |sort: 'date' %}

<!-- hidden table with all dates to be dsplayed on main page -->
<table id="cur_data" style="display: none;">
<thead>
    <tr><th>year</th><th>date</th><th>title</th><th>speaker</th><th>affiliation</th><th>location</th><th>content</th><th>url</th></tr>
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
		<td>{{ talk.url | prepend: site.baseurl }}</td>
	    </tr>
	{% endif %}
    {% endfor %}
</tbody>
</table>

<div id="events"></div>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script>
    var today = new Date()
		
    var first_future_talk = 0;
    $('#cur_data tbody tr').each(function(){
    var test = $(this).find('td:eq(1)').text();
    var test_date = new Date(test.replace(/-/g,'/'));
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
    
    $('#events').append("<h2>Upcoming Events</h2>");
    while(j < table.rows.length ){
	      cells = table.rows[j].cells;
	      year = cells[0].innerHTML;
	      dt = cells[1].innerHTML;
	      ttl = cells[2].innerHTML;
	      spkr = cells[3].innerHTML;
	      aff = cells[4].innerHTML;
	      loc = cells[5].innerHTML;
	      con = cells[6].innerHTML;
	      urll = "'"+cells[7].innerHTML+"'";
	      
	      dt_obj = new Date(dt.replace(/-/g,'/'));
	      day = dt_obj.getDate();
  	      mon = monthNames[dt_obj.getMonth()];
	      
	      if (year > year_old){
	          table_handle = 'future_'+year;
	          $('#events').append("<h3>"+year+"</h3>");
                  $('#events').append("<table id='"+table_handle+"' class='talks' style='overflow: hidden;display: table!important;margin-top:2em;margin-bottom:2em;'></table>");
	          year_old = year;
	      }
	      $('#'+table_handle).append("<tr onclick=\"location.href="+urll+"\"><td><b>"+spkr+"</b><span class='affil'> ["+aff+"] </span><span class='event_date'>"+day+" "+mon+", "+year+"</span><br><i>"+ttl+"</i><br><div id='abstractbox'>"+con+"</div></td></tr>");
	      j += 1;
	  }
    
    j = first_future_talk;
    year_old = table.rows[j].cells[0].innerHTML + 1;

    $('#events').append("<h2>Past Events</h2>");
    while(j >= 1){
	      cells = table.rows[j].cells;
	      year = cells[0].innerHTML;
	      dt = cells[1].innerHTML;
	      ttl = cells[2].innerHTML;
	      spkr = cells[3].innerHTML;
	      aff = cells[4].innerHTML;
	      loc = cells[5].innerHTML;
	      con = cells[6].innerHTML;
	      urll = "'"+cells[7].innerHTML+"'";

	      
	      dt_obj = new Date(dt);
	      day = dt_obj.getDate();
  	      mon = monthNames[dt_obj.getMonth()];
	      
	      if (year < year_old){
	          table_handle = 'past_'+year;
	          $('#events').append("<h3>"+year+"</h3>");
                  $('#events').append("<table id='"+table_handle+"' class='talks' style='overflow: hidden; display: table!important;margin-top:2em;margin-bottom:2em;'></table>");
	          year_old = year;
	      }
	      $('#'+table_handle).append("<tr onclick=\"location.href="+urll+"\"><td><b>"+spkr+"</b><span class='affil'> ["+aff+"] </span><span class='event_date'>"+day+" "+mon+", "+year+"</span><br><i>"+ttl+"</i><br><div id='abstractbox'>"+con+"</div></td></tr>");
	      j -= 1;
	  }
</script>

<a href="{{site.baseurl}}/archive">Archive</a>
