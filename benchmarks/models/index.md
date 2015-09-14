---
title: Models
layout: default
---

# Accepted Models

{% if site.data.accepted.size > 0%}
<table class="decoratedtable">
	<tr>
		<td>Name</td>
		<td>Description</td>
		<td>Link</td>
	</tr>
	{% for model in site.data.accepted %}
	<tr>
		<td>{{model.name}}</td>
		<td>{{model.description}}</td>
		<td>{{model.url}}</td>
	</tr>
	{% endfor %}
</table>
{% else %}
There are currently no accepted benchmark models
{% endif %}

# Models Under Submission

<table class="decoratedtable">
	<tr>
		<td>Name</td>
		<td>Description</td>
		<td>Link</td>
	</tr>
	{% for model in site.data.submit %}
	<tr>
		<td>{{model.name}}</td>
		<td>{{model.description}}</td>
		<td>{{model.url}}</td>
	</tr>
	{% endfor %}
</table>