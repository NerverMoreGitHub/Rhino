---
title: RhinoCommon Guides
description: RhinoCommon is the cross-platform .NET plugin SDK for Rhino.
platforms: ['Windows', 'Mac']
layout: guide-homepage
---


### Overview

- [What is RhinoCommon?]({{ site.baseurl }}/guides/rhinocommon/what_is_rhinocommon/)
- [What are Mono & Xamarin?]({{ site.baseurl }}/guides/rhinocommon/what_are_mono_and_xamarin/)

### Getting Started

- Installing Tools ([Windows]({{ site.baseurl }}/guides/rhinocommon/installing_tools_windows/), [Mac]({{ site.baseurl }}/guides/rhinocommon/installing_tools_mac/))
- Your First Plugin ([Windows]({{ site.baseurl }}/guides/rhinocommon/your_first_plugin_windows/), [Mac]({{ site.baseurl }}/guides/rhinocommon/your_first_plugin_mac/), [Cross-Platform]({{ site.baseurl }}/guides/rhinocommon/your_first_plugin_crossplatform/))
- Plugin Installers ([Windows]({{ site.baseurl }}/guides/rhinocommon/plugin_installers_windows/), [Mac]({{ site.baseurl }}/guides/rhinocommon/plugin_installers_mac/))

<!--column-->

### Fundamentals

<div class="trigger">
  {% assign guides = site.guide_topics | sort:"order" %}
  <ul>
  {% for guide in guides %}
    {% if guide.apis contains 'RhinoCommon' and guide.categories contains 'Fundamentals' %}
      {% if guide.title and guide.order %}
        <li><a class="page-link" href="{{ guide.url | prepend: site.baseurl }}" title="{{ guide.description }}">{{ guide.title }}</a></li>
      {% endif %}
    {% endif %}
  {% endfor %}
  </ul>
</div>

### Advanced

<div class="trigger">
  {% assign guides = site.guide_topics | sort:"order" %}
  <ul>
  {% for guide in guides %}
    {% if guide.apis contains 'RhinoCommon' and guide.categories contains 'Advanced' %}
      {% if guide.title and guide.order %}
        <li><a class="page-link" href="{{ guide.url | prepend: site.baseurl }}" title="{{ guide.description }}">{{ guide.title }}</a></li>
      {% endif %}
    {% endif %}
  {% endfor %}
  </ul>
</div>

<!--column-->

### Zoo

<div class="trigger">
  {% assign guides = site.guide_topics | sort:"order" %}
  <ul>
  {% for guide in guides %}
    {% if guide.apis contains 'RhinoCommon' and guide.categories contains 'Zoo' %}
      {% if guide.title and guide.order %}
        <li><a class="page-link" href="{{ guide.url | prepend: site.baseurl }}" title="{{ guide.description }}">{{ guide.title }}</a></li>
      {% endif %}
    {% endif %}
  {% endfor %}
  </ul>
</div>
