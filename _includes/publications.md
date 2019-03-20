{% for paper in site.data.papers %}
{% if paper.authors contains include.author_id %}

{% assign author_links = "" | split: "" %}
{% for author_id in paper.authors %}

  {% capture link %}{% include person_link.md person_id=author_id %}{% endcapture %}
  {% assign link = link | strip %}

  {% if paper.cofirst_authors contains forloop.index %}
    {% assign link = link | append: "\*" %}
  {% endif %}

  {% assign author_links = author_links | push: link %}
{% endfor %}

- **{{ paper.title }}**.

  {{ author_links | join: ", " }}{% if paper.cofirst_authors %} (\*: co-first authors in alphabetical order){% endif %}.

  {{ paper.venue }}, **{{ paper.year }}**{% if paper.status %} ({{ paper.status }}){% endif %}.

  {% if paper.copy_local %}\[[paper]({{ paper.copy_local }})\]{% endif %}
  {% if paper.website %}\[[project page]({{ paper.website }})\]{% endif %}
  {% if paper.copy_publisher %}\[[publisher's page]({{ paper.copy_publisher }})\]{% endif %}

  <br />

{% endif %}
{% endfor %}