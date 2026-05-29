---
layout: page
permalink: /repositories/
title: repositories
description: Open-source code and selected GitHub repositories.
nav: true
nav_order: 8
---

<style>
  .repo-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.25rem;
    margin-top: 1.25rem;
    margin-bottom: 2rem;
  }

  .repo-card {
    display: flex;
    flex-direction: column;
    border: 1px solid var(--global-divider-color);
    border-radius: 0.5rem;
    padding: 1.1rem 1.25rem;
    background-color: var(--global-card-bg-color);
    transition: border-color 0.2s ease, transform 0.2s ease;
    text-decoration: none;
  }

  .repo-card:hover {
    border-color: var(--global-theme-color);
    transform: translateY(-2px);
  }

  .profile-card {
    flex-direction: row;
    align-items: center;
    gap: 1rem;
  }

  .profile-card img {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    flex-shrink: 0;
  }

  .repo-card .repo-title {
    font-weight: 600;
    color: var(--global-theme-color);
    margin-bottom: 0.4rem;
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }

  .repo-card .repo-desc {
    font-size: 0.85rem;
    line-height: 1.45;
    color: var(--global-text-color);
    opacity: 0.8;
    margin-bottom: 0.75rem;
  }

  .repo-card .repo-meta {
    margin-top: auto;
    font-size: 0.78rem;
    color: var(--global-text-color);
    opacity: 0.65;
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }

  .repo-card .repo-lang-dot {
    width: 0.65rem;
    height: 0.65rem;
    border-radius: 50%;
    background-color: var(--global-theme-color);
    display: inline-block;
  }

  .profile-card .profile-name {
    font-weight: 600;
    color: var(--global-text-color);
  }

  .profile-card .profile-handle {
    font-size: 0.85rem;
    color: var(--global-theme-color);
  }
</style>

{% if site.data.repositories.github_users %}

## GitHub

<div class="repo-grid">
  {% for user in site.data.repositories.github_users %}
  <a class="repo-card profile-card" href="https://github.com/{{ user }}" target="_blank" rel="external nofollow noopener">
    <img src="https://github.com/{{ user }}.png" alt="{{ user }}" loading="lazy">
    <div>
      <div class="profile-name">{{ site.first_name }} {{ site.last_name }}</div>
      <div class="profile-handle">@{{ user }}</div>
    </div>
  </a>
  {% endfor %}
</div>

{% endif %}

{% if site.data.repositories.github_repos %}

## Repositories

<div class="repo-grid">
  {% for repo in site.data.repositories.github_repos %}
  <a class="repo-card" href="https://github.com/{{ repo.name }}" target="_blank" rel="external nofollow noopener">
    <div class="repo-title">
      <i class="fa-solid fa-book-bookmark"></i>
      {{ repo.title | default: repo.name }}
    </div>
    {% if repo.description %}<div class="repo-desc">{{ repo.description }}</div>{% endif %}
    {% if repo.language %}<div class="repo-meta"><span class="repo-lang-dot"></span>{{ repo.language }}</div>{% endif %}
  </a>
  {% endfor %}
</div>

{% endif %}
