---
layout: splash
permalink: /
title: "TOPIK Practice Bank"
header:
  overlay_color: "#1e3932"
excerpt: "Original TOPIK I & II practice questions with clear English explanations. Learn every question type, then test yourself."
intro:
  - excerpt: "Pick your level and learn one question type at a time."
feature_row:
  - title: "TOPIK I (Level 1-2)"
    excerpt: "Reading question types for beginners, explained step by step with original practice questions."
    url: "/topik-i/"
    btn_label: "Start TOPIK I"
    btn_class: "btn--primary"
  - title: "TOPIK II (Level 3-6)"
    excerpt: "Reading and writing strategies for intermediate and advanced learners, including Writing 51-54."
    url: "/topik-ii/"
    btn_label: "Start TOPIK II"
    btn_class: "btn--primary"
  - title: "Free Mini Tests"
    excerpt: "Short printable PDF tests with an answer key and English explanations. No sign-up needed."
    url: "/free/"
    btn_label: "See Free Tests"
    btn_class: "btn--inverse"
---

{% include feature_row id="intro" type="center" %}

{% include feature_row %}

## Latest question-type guides

{% for post in site.posts limit:6 %}
- [{{ post.title }}]({{ post.url | relative_url }}) <small>{{ post.date | date: "%b %-d, %Y" }}</small>
{% endfor %}

## Practice bank

All questions on this site and in our practice books are **original**. We study each official question type and write new passages, dialogues and answer choices from scratch.

[Browse the shop]({{ "/shop/" | relative_url }}){: .btn .btn--primary .btn--large}
