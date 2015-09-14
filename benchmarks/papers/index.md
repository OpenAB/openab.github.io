---
title: Papers
layout: default
---

# Papers

The following list of papers are user contributed resources which either give insight into multi agent simulator performance, benchmarking procedures in other domains or details of benchmark models. If you would like to contribute a paper then please [contact us](../../contact/).

<table>
	<tr>
		<td>Papers</td>
	</tr>
	{% for paper in site.data.papers %}
	<tr> 
		<td>
		<p>"{{paper.title}}", {{paper.author-list}}. <i>{{paper.publication}}</i> (<a href='{{paper.url}}'>link</a>)</p>
		<p>{{paper.description}}</p>
		<p>Keywords: {{paper.keywords}}</p>
		</td>
	</tr>
	{% endfor %}
</table>