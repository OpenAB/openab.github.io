---
title: Simulators
layout: default
---

# Simulators

The following list of simulators are suitable for the distributed and parallel simulation of multi agent systems models. They are the current recommended reference simulators required for the [submission processes](../submission/) of benchmark models. If you would link to submit your simulator to this list of reference simulators then please [contact us](../../contact/).

<table class="decoratedtable">
	<tr>
		<th>Simulator</th>
		<th>Description</th>
		<th>Website</th>
	</tr>
	{% for sim in site.data.simulators %}
	<tr>
		<td>{{sim.name}} 
		{% if sim.img %}
			</br>
			<img src='{{sim.img}}' alt='{{sim.name}}' width='50px'>
		{% endif %}
		</td>
		<td>{{sim.description}}</td>
		<td><a href="http://{{sim.url}}">{{sim.url}}</td>
	</tr>
	{% endfor %}
</table>
