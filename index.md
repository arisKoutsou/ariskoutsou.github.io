---
layout: default
title: Home
---

<div class="page-layout">
  <aside class="sidebar">
    <figure class="profile-card">
      <img src="{{ site.data.profile.photo }}" alt="Portrait of {{ site.data.profile.name }}" />
    </figure>
    <div class="sidebar-info">
      <h1>{{ site.data.profile.name }}</h1>
    </div>
    <ul class="profile-meta" aria-label="Profile information">
      <li class="meta-item institute"><span class="meta-icon" aria-hidden="true">🏛️</span>
        {% if site.data.profile.affiliation_url %}
          <a href="{{ site.data.profile.affiliation_url }}">{{ site.data.profile.affiliation }}</a>
        {% else %}
          {{ site.data.profile.affiliation }}
        {% endif %}
      </li>
      <li class="meta-item location"><span class="meta-icon" aria-hidden="true">📍</span>{{ site.data.profile.location }}</li>
      <li class="meta-item email"><span class="meta-icon" aria-hidden="true">✉️</span><a href="mailto:{{ site.data.profile.email }}" title="Email">email</a></li>
      {% if site.data.profile.github %}
        <li class="meta-item github"><img class="meta-icon meta-icon-image" src="/assets/icons/github-invertocat-black-clearspace.svg" alt="" aria-hidden="true" /><a href="{{ site.data.profile.github }}">GitHub</a></li>
      {% endif %}
      {% if site.data.profile.linkedin %}
        <li class="meta-item linkedin"><img class="meta-icon meta-icon-image" src="/assets/icons/linkedin-inbug-black.png" alt="" aria-hidden="true" /><a href="{{ site.data.profile.linkedin }}">LinkedIn</a></li>
      {% endif %}
    </ul>
  </aside>

  <main class="main-content">
    <section class="panel" id="bio">
      {{ site.data.profile.bio | markdownify }}
      {{ site.data.profile.long_bio | markdownify }}
    </section>

    <section class="panel" id="publications">
      <h2>Publications</h2>
      <div class="card-list">
        {% for item in site.data.publications %}
          <article class="list-card">
            <p class="meta">{{ item.year }}{% if item.venue %} · {{ item.venue }}{% endif %}</p>
            {% assign doi_link = nil %}
            {% assign slides_link = nil %}
            {% for link in item.links %}
              {% if link.label == 'DOI' or link.label == 'doi' %}
                {% assign doi_link = link.url %}
              {% endif %}
              {% if link.label == 'Slides' or link.label == 'slides' %}
                {% assign slides_link = link.url %}
              {% endif %}
            {% endfor %}
            {% if doi_link %}
              <h3>
                <a href="{{ doi_link }}">{{ item.title }}</a>
                {% if slides_link %}&nbsp;[<a href="{{ slides_link }}" target="_blank" rel="noopener noreferrer">slides</a>]{% endif %}
              </h3>
            {% else %}
              <h3>
                {{ item.title }}
                {% if slides_link %}&nbsp;[<a href="{{ slides_link }}" target="_blank" rel="noopener noreferrer">slides</a>]{% endif %}
              </h3>
            {% endif %}
            <p>{{ item.authors }}</p>
            {% if item.links %}
              <p class="inline-links">
                {% for link in item.links %}
                  {% unless link.label == 'DOI' or link.label == 'doi' or link.label == 'Slides' or link.label == 'slides' %}
                    <a href="{{ link.url }}">{{ link.label }}</a>
                  {% endunless %}
                {% endfor %}
              </p>
            {% endif %}
          </article>
        {% endfor %}
      </div>
    </section>

    <section class="panel" id="teaching">
      <h2>Teaching assistant</h2>
      <div class="card-list">
        {% for item in site.data.teaching %}
          <article class="list-card">
            <p class="meta">{{ item.period }}</p>
            <h3>
              {% if item.course_url %}
                <a href="{{ item.course_url }}">{{ item.course }}</a>
              {% else %}
                {{ item.course }}
              {% endif %}
              {% if item.professor %}
                with
                {% if item.professor_url %}
                  <a href="{{ item.professor_url }}">{{ item.professor }}</a>
                {% else %}
                  {{ item.professor }}
                {% endif %}
                at
                {% if item.institution_url %}
                  <a href="{{ item.institution_url }}">{{ item.institution }}</a>
                {% else %}
                  {{ item.institution }}
                {% endif %}
              {% endif %}
            </h3>
            <p>{{ item.role }}</p>
          </article>
        {% endfor %}
      </div>
    </section>

    <section class="panel" id="blogposts">
      <h2>Blog posts</h2>
      <div class="card-list">
        {% for post in site.data.blogposts %}
          <article class="list-card {% if post.type == 'external' %}external{% endif %}">
            <p class="meta">{{ post.date | date: "%B %Y" }}</p>
            <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
            <p>{{ post.summary }}</p>
          </article>
        {% endfor %}
      </div>
    </section>
  </main>
</div>
