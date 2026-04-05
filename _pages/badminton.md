---
title: "Badminton"
permalink: /badminton/
author_profile: true
---

<style>
.badminton-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}
.badminton-card {
  border: 1px solid #e5e7eb;
  border-radius: 0.75rem;
  overflow: hidden;
  background: #fff;
  box-shadow: 0 3px 12px rgba(0, 0, 0, 0.08);
}
.badminton-card a {
  text-decoration: none;
  color: inherit;
  display: block;
}
.badminton-media {
  width: 100%;
  aspect-ratio: 16 / 10;
  background: #f3f4f6;
  overflow: hidden;
}
.badminton-media img,
.badminton-media video,
.badminton-media iframe {
  width: 100%;
  height: 100%;
  display: block;
  object-fit: cover;
  border: 0;
}
.badminton-title {
  margin: 0;
  padding: 0.85rem 0.95rem 1rem;
  font-size: 1rem;
  line-height: 1.35;
}
.badminton-empty {
  color: #6b7280;
  font-style: italic;
}
</style>

{% assign tournaments = site.badminton | sort: "date" | reverse %}

{% if tournaments and tournaments.size > 0 %}
<div class="badminton-gallery">
  {% for tournament in tournaments %}
  <article class="badminton-card">
    <a href="{{ tournament.url | relative_url }}">
      <div class="badminton-media">
        {% if tournament.card_type == "video" and tournament.card_video %}
          {% assign card_video = tournament.card_video %}
          {% if card_video contains "youtube.com/embed/" or card_video contains "player.vimeo.com/" %}
            <iframe src="{{ card_video }}" title="{{ tournament.title }}" loading="lazy" allowfullscreen></iframe>
          {% elsif card_video contains ".mp4" or card_video contains ".webm" or card_video contains ".ogg" %}
            {% if card_video contains "://" %}
              <video controls preload="metadata" playsinline>
                <source src="{{ card_video }}" type="video/mp4">
              </video>
            {% else %}
              <video controls preload="metadata" playsinline>
                <source src="{{ card_video | relative_url }}" type="video/mp4">
              </video>
            {% endif %}
          {% else %}
            {% if tournament.card_image %}
              {% if tournament.card_image contains "://" %}
                <img src="{{ tournament.card_image }}" alt="{{ tournament.title }}">
              {% else %}
                <img src="{{ tournament.card_image | relative_url }}" alt="{{ tournament.title }}">
              {% endif %}
            {% else %}
              <img src="{{ '/images/500x300.png' | relative_url }}" alt="{{ tournament.title }}">
            {% endif %}
          {% endif %}
        {% else %}
          {% if tournament.card_image %}
            {% if tournament.card_image contains "://" %}
              <img src="{{ tournament.card_image }}" alt="{{ tournament.title }}">
            {% else %}
              <img src="{{ tournament.card_image | relative_url }}" alt="{{ tournament.title }}">
            {% endif %}
          {% else %}
            <img src="{{ '/images/500x300.png' | relative_url }}" alt="{{ tournament.title }}">
          {% endif %}
        {% endif %}
      </div>
      <h3 class="badminton-title">{{ tournament.title }}</h3>
    </a>
  </article>
  {% endfor %}
</div>
{% else %}
<p class="badminton-empty">No badminton tournament posts yet. Add markdown files in <code>_badminton/</code>.</p>
{% endif %}
