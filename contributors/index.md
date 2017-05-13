---
title: Contributors
index: false
---

# Contributors

If you contribute to ConstraintLayout.com, just create a pull request and submit it to us. 
You can also file an [issue](https://github.com/ConstraintLayout/constraintlayout.github.io/issues). 


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
