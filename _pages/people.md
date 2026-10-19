---
layout: page
title: group
permalink: /people/
description: Current and former members of the research group at the Department of Earth Sciences, Uppsala University.
nav: true
nav_order: 4
---

{%- assign groups = "postdocs,phd_students,visiting" | split: "," -%}
{%- assign headings = "Postdoctoral Researchers,PhD Students,Visiting PhD Students" | split: "," -%}
{%- for group in groups -%}
{%- assign members = site.data.people[group] -%}
{%- if members and members.size > 0 %}

<h2>{{ headings[forloop.index0] }}</h2>
<ul class="people-grid">
{%- for person in members %}
<li class="person">
{%- if person.image %}
<img src="{{ '/assets/img/people/' | append: person.image | relative_url }}" alt="{{ person.name }}" loading="lazy">
{%- endif %}
{% if person.website -%}
<a class="person-name" href="{{ person.website }}">{{ person.name }}</a>
{%- else -%}
<span class="person-name">{{ person.name }}</span>
{%- endif %}
{%- if person.description %}
<span class="person-focus">{{ person.description }}</span>
{%- endif %}
{%- if person.affiliation %}
<span class="person-focus">{{ person.affiliation }}</span>
{%- endif %}
<span class="person-focus">Since {{ person.years | split: "–" | first }}</span>
</li>
{%- endfor %}
</ul>
{% endif -%}
{%- endfor %}

---

## Alumni

### PhD Students

<ul class="alumni-list">
{%- for person in site.data.people.alumni_phd %}
<li>{{ person.years }} ({{ person.role }}) {{ person.name }}, {{ person.affiliation }}, <em>{{ person.topic }}</em></li>
{%- endfor %}
</ul>

### Postdoctoral Researchers

<ul class="alumni-list">
{%- for person in site.data.people.alumni_postdoc %}
<li>{{ person.years }} ({{ person.role }}) {{ person.name }}</li>
{%- endfor %}
</ul>

### Visiting PhD Students

<ul class="alumni-list">
{%- for person in site.data.people.alumni_visiting %}
<li>{{ person.years }} {{ person.name }}, {{ person.affiliation }}{% if person.topic %}, <em>{{ person.topic }}</em>{% endif %}</li>
{%- endfor %}
</ul>

### Master's Thesis Students

<ul class="alumni-list">
{%- for person in site.data.people.alumni_msc %}
<li>{{ person.name }}, <em>{{ person.title }}</em>, {{ person.year }}</li>
{%- endfor %}
</ul>
