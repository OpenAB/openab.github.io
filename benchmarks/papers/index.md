---
title: Papers
layout: default
---

# Papers

The following list of papers are user contributed resources which either give insight into multi agent simulator performance, benchmarking procedures in other domains or details of benchmark models. If you would like to contribute a paper then please [contact us](../../contact/).

<ul class="list-of-papers">
	{% for paper in site.data.papers %}
	<li> 
		<h3>"{{paper.title}}"</h3>
		<h4>{{paper.author-list}}</h4>
		<p class="publication">{{paper.publication}}</p>
		<p class="keywords">
			<span>Keywords:</span>
			{{paper.keywords}}
		</p>
		<p class="description">{{paper.description}}</p>
		{% if paper.url || paper.bib %}
			{% if paper.url %}
				<a class="paper-button" href="{{paper.url}}">link</a>
			{% endif %}
			{% if paper.bib %}
				<a class="paper-button" href="{{paper.bib}}">cite</a>
			{% endif %}
		{% endif %}
		{% if paper.abstract %}
			<input class="abstract-toggle" type="checkbox" id="abstract-toggle-{{forloop.index}}" />
			<label class="paper-button" for="abstract-toggle-{{forloop.index}}">Abstract</label>
		{% endif %}
		<p class="abstract">{{paper.abstract}}</p>
	</li>
	{% endfor %}
</ul>
