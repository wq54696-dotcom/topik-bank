---
permalink: /subscribe/
title: "Subscribe"
excerpt: "New free tests and subscriber-only discounts, about twice a month."
---

Subscribers get:

- A new free mini test every month
- Early access and a discount code for new practice banks
- TOPIK schedule reminders

<!--
구독 연결 방법 (둘 중 하나)
A. Gumroad 팔로우: 아래 버튼 링크를 본인 Gumroad 프로필 주소로 바꾸면 끝
B. MailerLite: 가입 후 만든 구독 폼의 HTML 코드를 이 자리에 붙여넣기
-->

{% if site.gumroad_store != "" %}
[Follow on Gumroad]({{ site.gumroad_store }}){: .btn .btn--primary .btn--large}

No spam. Unsubscribe anytime.
{% else %}
**Sign-up opens soon.** In the meantime, grab the [free mini tests]({{ "/free/" | relative_url }}) and the [question-type guides]({{ "/lessons/" | relative_url }}).
{% endif %}
