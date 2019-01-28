# Website Documentation

## Table of Contents

0. [How to Use This Wiki](#wiki)

1. [General](#general)

2. [Banner Images](#banner)

3. [Mission Statement](#mission)

4. [Research](#research)

5. [Team](#team)

6. [Publications](#publications)

7. [News](#news)

8. [Events](#events)

9. [Jobs, Contact and Downloads](#rest)

10. [Impressum](#impressum)

11. [Notes for the Webmaster](#notes)

<a name="wiki"></a>
## 2. How to Use This Wiki

You don't have to read all of this if you want to make a change or contribution to the site. Just read [1. General](#general) and then skip over to the sections that relates to what you want to do. Some of them reference do other sections at which you then can take a look if needed. However, please **do not omit reading the general information**, as it will prevent easily avoidable errors.

<a name="general"></a>
## 1. General

The website is built using **Jekyll**, a Ruby based static website generator. It makes use of **YAML**, **markdown** and **LiquidScript** to generate websites. The use of YAML and markdown makes it easy to edit and create content for the website without coding explicit html.

You can find the documentation of Jekyll [here](https://jekyllrb.com/docs/), the YAML documentation [here](https://jekyllrb.com/docs/front-matter/) and the LiquidScript documentation [here](https://jekyllrb.com/docs/liquid/).

Now follows a simple example of YAML and markdown:

```yaml/markdown
---
layout: member_post
title: Denis Alevi
img: "denis_crop.JPG"
position: Master Student
permalink: /denis/
room: MAR 5.014
email: denis.alevi@bccn-berlin.de
---
Denis Alevi studied Physics at Heidelberg University, where he worked on
Neuromorphic Hardware for his bachelor's thesis. Currently he is pursuing a
master's degree in Computational Neuroscience at the Bernstein Center in Berlin
and joined the lab in 2017. For his master's thesis he is trying to
understand how biologically motivated constraints to network architectures can
lead to episodic to semantic memory transformations in a mechanistic model of
systems memory consolidation. To this end, he uses methods from machine
learning, computational models from neuroscience and mathematical analysis.
Denis is also interested in algorithms for simulating spiking neural networks
on graphics processing units and has developed the open source software
Brian2CUDA.
```

The part between the '---' characters is the YAML header. It allows to define variables that are later used to generate a page. The variable names come before the colon and the value that they hold come after. These are going to be used by Jekyll to automatically create Denis' member page in this example. It is important to use the correct syntax here - `variable: value` for simple variables. If the vaule contains certian reserved characters like for example "-", the whole value should be enclosed in quotation marks. Another syntactic feature of YAML that we use are lists. They are structured as follows:
```
list:
    - item1
    - item2
    ...
```
It is crucial that there is always a whitespace after the "-", otherwise this will not be recognized as a list.

The part below is markdown, which is basically just text, but where you can also insert links and images and tables and so on. We are mostly using it for text and for the fact that when html is generated from it, formatting is preserved.

**Important formatting note**: As mentioned above, certain characters within a YAML header are reserved and will not be displayed correctly when used, or even break the file structure and cause deployment of the site to fail. In such cases, check if the error goes away by removing special characters. If it does, there are various ways to prevent this kind of behavior, the simplest one being to enclose the value in question in ""-quotes. Some other ways are outlined [here](https://interviewbubble.com/solved-how-to-escape-indicator-characters-or-in-yaml-escaping-colons-in-yaml/), particularily if you want to use line breaks for some reason. However, tread carefully and always test, because Jekyll does not fully support all of these.

If you add new images, please use compression (I used [this](https://tinypng.com/) site that works with jpg and png images) in order to save some loading time.

<a name="banner"></a>
## 2. Banner Images

For all except the home page the banner images should be located in `assets/img/banners` . Then we need to indicate that we want to use a particular image in that folder in the file corresponding to the page we want to use it on. All page-files are located in the folder `pages`. Now if we want to change the banner of the news page for example, we open `news.md` and edit (or add, if it doesn't exist) the line

```yaml
banner-img: "news_image.JPG"
```

where news_image.JPG is the desired image that we put in the `assets/img/banners` folder.

For the home page, to change the image we edit the `banner-img ` entry of `index.html` the same way described above.

<a name="mission"></a>
## 3. Mission Statement

To change the Mission Statement, open `_config.yml` and edit the line `text: `.

<a name="research"></a>
## 4. Research

### Projects

All research projects are located in the folder `_research/`. They are then displayed on the research page onw below the other. Let us look at an example:

```yml/markdown
---
layout: page
title: Burst  Control  in  Cortical  Circuits 
image: "diag_filip.jpg"
parents:
    - Inhibition
    - Plasticity
authors:
    - Filip Vercruysse
---
The  existence  of  specialized  mechanisms  for  burst  generation  in  pyramidal  cells  (PCs)  suggests  that  bursts  are  likely  to  be  an  important  temporal  feature  of  neural  signals.  In L5  PCs  bursts  occur  at  a  low,  but  consistent  rate,  and  are  thought  to  arise  from  active  dendritic  processes.  Given  that  burst  activity  relies  on  dendritic  threshold  mechanisms,  it  appears  likely  that  low  burst  activity  require  homeostatic  control,  but  the  underlying  mechanisms  are  not  resolved.  In  this  research  project  we  model  a  biologically  inspired  circuit  diagram  of  a  self-organized  microcircuit  with  different  inhibitory  cell  types  and  plasticity  rules  to  control  the  burst  and  population  rate  of  PCs.  Our  work  shows  that  inhibitory  plasticity  rules  may  serve  as  building  blocks  to  self-organise  complex  network  architectures  and  allows  us  to  investigate  coding  properties  of  bursting  units  without  the  need  for  tuning  of  input  or  noise  levels. 
  
```

`layout` should always be set to 'page'. The `title` is obviously the title of the project. `image` holds the name of the image displayed with the project. All project images should be placed in the `assets/img/research` folder.

`parents` is a list of either one or two items from the categories listed in the file `pages/1_research.md` under headings: 'Inhibition', 'Plasticity' and 'Behavior'. Please note that a poject cannot have both 'Inhibition' and 'Behavior' as parents. They serve to subdivde the project page into these four subcategories; failing to match one of these keywords means that the project will not be displayed.

`authors` is a list of authors that work on the project. These names should exactly correspond with the `title` entry of a file in the `_members` folder, or in other words, exactly match a name of a member of the group as used on the team page.

The markdown contains a description of the project.

To create a new project, just create a new file with this structure in the `_research/` folder.

### Navigation Categories (Research Headings)

To change the research project categories 'Inhibition', 'Plasticity' and 'Behavior', edit  the `headings` entry of `pages/1_research.md`. Do not forget the whitespace before the '-'! Note that this is a far reaching change as you then have to also change the parents of all research projects to reflect the change you made here.

<a name="team"></a>
## 5. Team

### Member Entries

For each team member there is a file in `_members`. All of these have a YAML header that looks like this:

```yaml
---
layout: member_post
title: Denis Alevi
img: "denis_crop.JPG"
position: Master Student
permalink: /denis/
room: MAR 5.014
email: denis.alevi@bccn-berlin.de
tel: +49 123456789
---
```

The layout is always set to "member_post", the `title` is the name of the person. The `image` entry should be set the name of the desired image (which should be put into the folder `assets/img/members`). These images also should have a height to width ratio of approximately 10:9 (all the current ones are 1000x900px). The `position` entry denotes the position of the person within the group. Currently available are 'Principal Investigator', 'Secretary', 'Postdoctoral Fellow', 'PhD Student', 'Master Student' and 'Alumnus' (set under `position-order` in `pages/2_team.md`). This entry determines the position title displayed under the member's name, as well as where the member will be displayed, as they are displayed in `position-order`, i.e. first the Principal Investigator, then the Secretary, then all Postdoctorall Fellows and so on. If a position is used that is not in the list, the member will be displayed last, in aplhabetical order, unless that position is "Aluimni" - in that case the member will appear in the Alumni-section. If the position exists in the list, it shoud be matched exactly here. The `permalink` denotes the link under which this site is going to be reachable, i.e. `sprekelerlab.net/denis/` in this case. `room`, `tel` and `email` are optional and self-explanatory.

The markdown part afterwards is the short bio of the person in question and is later displayed on their page.

### Alumni
One special position is Alumni (yes, I know that the proper singular is Alumnus/Alumna). If `position: Alumnus` is specified, the member does not appear with all the others as described above, but instead at the very bottom in a special Alumni-grid. When edition the position order (see next section) it is crucial that "Alumni" is **not** part of that list!

### Position Order
To change the order of positions within the group, edit `position-order` in `pages/2_team.md`. It is also possible to add or remove position entries. Everything not on this list is displayed last in alphabetical order.

<a name="publications"></a>
## 6. Publications

All publications haven an entry in `_data/publications.json`, which contains a list of dictionaries , each of which corresponds to a publication. An entry looks like this:

```{
{
    "title": "Sparse bursts optimize information transmission in a multiplexed neural code",
    "author": "R. Naud, H. Sprekeler",
    "year": "2018",
    "journal": "PNAS, 115(27):E6329-E6338",
    "link" : "chrome-extension://oemmndcbldboiebfnladdacbdfmadadm/http://www.pnas.org/content/pnas/early/2018/06/21/1720995115.full.pdf"
}
```

Edit and create new entries at your heart's delight (while preserving the correct syntax of course).

The publications are later automatically sorted by year, but **within a year the order within the file is preserved**.

### Preprints

A publication can be marked as a preprint by adding the line `"preprint": "true"` to its json entry. If this line is absent, it is simply assumed that the paper in question is not a preprint and the site will deploy correctly. Preprints are listed at the very top of the page under the heading (surprise!) "Preprints". Obviously, once the the paper gets published, the preprint entry has to be removed manually.

<a name="news"></a>
## 7. News

News posts are all located in `_posts/`.  The name of the file always follows the following convention: `year-month-day-title.md`, for example `2013-11-18-im-a-blog-post.md`. The date is important and used for the date displyaed with the post, the title is not as it is set within the YAML header of the file for formatting reasons.

Each such file has a YAML header:

```yaml
---
layout: post
title: Feature images
thumbnail: "desk-messy.jpeg"
---
```

The layout is always post. The title is the title of the post. The `thumbnail` is optional and should  be set to the name of the desired image (which should be placed in the folder `assets/img/thumbnails`).

The markdown after the YAML header contains the content of the news post.

To make a new news post, simply create or copy a file with this structure and edit it to your expectations.

<a name="events"></a>
 ## 8. Events

Each event has its own file, and all of those are located in `_talks`.  The name of the file always follows the following convention: `year-month-day-lastname-firstname.md`, for example `2013-11-18-jones-sarah.md`.

The YAML header of these `.md` files looks like this:

```yaml
---
layout: post_event
title: The Cost of Control in Perceptual Decision Making
date: July 04, 2020, 18:00
speaker: Alfonso Renart
location: MAR 1002.356
affiliation: Champalimaud
priority: September 18, 2018
---
```

layout is always set to 'post_event'. `title`, `date`, `speaker`, `location` and `affiliation` (of the speaker) are self-explanatory. **It is important that the date (which can, but does not have to contain a time) is always written in the same format (as written above).** Note that in `date` the time `00:00` will not work (it will not get displayed).

`priority` is an optional entry that requires some more explanation. The home page of the website always displays the three next events. Usually that is good enough, but sometimes we want to advertise important events early, even if they lie far in the future and are not among the three next ones. In that case we can set priority to a date, and after this date passes, this event is considered as having priority, meaning that is is displayed on the home page regardless of how far in the future it lies.

<a name="rest"></a>
## 9. Jobs, Contact and Downloads

To change the contents of the jobs page, simply edit the markdown portion of  `pages/6_jobs.md`. 

The same goes for Downloads, the file is `pages/8_downloads.md`.

The contact file ( `pages/7_contact.md`) is written in html. To edit it, simply edit the text according to html-conventions.

<a name="impressum"></a>
## 10. Impressum

To change the impressum page, edit `pages/impressum.md` (plain markdown).

<a name="notes"></a>
## 11. Notes for later Webmasters
I hope that I leave the website in a readable and maintainable state for you. I you, like me, are not an expert at webdesign, and if you havent done so already, familiarize yourself with the tools used to create this website, as discribed under [General](#general), most importantly Jekyll. This section is not intended as an exhaustive explanation of every detail about how the site works, but more of a primer of its structure.

### HTML and Organization
Most of the pages are generated from the folder `pages`. Files there might use a YAML entry `layout` which specifies a layout that you will find in the `_layouts` folder. Also they might use additional external HTML file with the liquid statement `{% include file_xy.html %}`. You will find these include-files in `_includes`.
Additionally, pages are generated from files in co-called collections. These collections are declared in `_config.yml` as follows:
```yaml
# COLLECTIONS
collections:
  members:
    output: true
    permalink: /:collection/:name
  talks:
    output: true
    permalink: /:collection/:name
  research:
    output: true
    permalink: /:collection/:name
```
You see that `_members` `_talks` and `_research` are folders declared as collections. Which means that from every `.md` file in them   will create a html file that will be served once the site is deployed. Everything about layouts and inclueds applies here as well.

All html pages except `index.html` are generated from `.md` files. As explained above, these files may have a YAML header in which varaibles to be used later can be specified. Under the YAML header there can be formatted text, html, javascript and liquidscript. For details, consult the documentations of these langauges and Jekyll.

### CSS
All of the custom css (except where it has to be used inline) is in either `_sass/_includes` or `_sass/_layouts`. Those files are registered in `_sass/type-on-strap.scss` and are combined into one big `.css` file before deployment, meaning that the css there affects all pages, not just the one they share a name with.

Usually the `.scss` file has the same name as the `md/html` file where it is used, except in cases where the same css in used in multiple files. It should be intuitive what file that is - if not, simply search through `_sass/_includes` and `_sass/_layouts` to find the class you are looking for.

### JS
Custom Javascript is used on four occasions - on `pages/5_events.md` (and `pages/events-archive.md`) to couple the visual effects of the authornames- and images throighout the site. Also, it is used on `pages/4_events.md` in conjunction with the `truncate`-class to make the show more/show less- button work. The final two times are to separate past from future dates on the home page and on the events page. To this end, an invisible table with all eventsd down to a certain cutoff-date in the past is created with liquidscript (in order to make use of Jekyll's YAML-parsing abilities) and then JS is used to separate past from future and put the correct events where they belong.
