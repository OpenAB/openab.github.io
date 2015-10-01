---
title: Simulators
layout: default
---

# Simulators

The following list of simulators are for the distributed and parallel simulation of multi agent systems models. They are the current reference simulators required for the [submission processes](../submission/) of benchmark models. If you would link to submit your simulator to this list of reference simulators then please [contact us](../../contact/).

<table class="decoratedtable">
	<tr>
		<td>Simulator</td>
		<td>Description</td>
		<td>Website</td>
	</tr>
	{% for sim in site.data.simulators %}
	<tr>
		<td>{{sim.name}}</td>
		<td>{{sim.description}}</td>
		<td><a href="http://{{sim.url}}">{{sim.url}}</td>
	</tr>
	{% endfor %}
</table>
