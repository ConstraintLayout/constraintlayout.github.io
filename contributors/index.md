---
title: Contributors
---

# Contributors

## Admins

{% assign contributor_pages = site.pages | where: "layout", "contributor" %}
{% for contributor_page in contributor_pages %}
{% if contributor_page.admin == true %}
  <ul>
    <li>
      <a href="{{ contributor_page.name | remove: '.md' | append: '.html' | prepend: 'contributors/' | relative_url }}">
        {{ contributor_page.forename }} {{ contributor_page.surname }}
      </a>
    </li>
  </ul>
{% endif %}
{% endfor %}
## Authors
{% for contributor_page in contributor_pages %}
{% if contributor_page.admin != true %}
  <ul>
    <li>
      <a href="{{ contributor_page.name | remove: '.md' | append: '.html' | prepend: 'contributors/' | relative_url }}">
        {{ contributor_page.forename }} {{ contributor_page.surname }}
      </a>
    </li>
  </ul>
{% endif %}
{% endfor %}
