---
layout: page
title: Measurement traffic
---

# Measurement traffic

If you are encountering problems with our anycast measurements, please read on to learn what to expect from us, how to reach out to us, and, as a last resort, how to block our traffic.
We thank you in advance for working with us to resolve any issues, and apologize in advance if we have inadvertently caused problems through our measurement.

## What traffic to expect?

Our measurements consist of a series of TCP, UDP, or ICMP packets sent to at most one IP address per /24 prefix. All packets are spaced at least 1 second apart. The order in which prefixes are selected is random to minimize load to larger networks.
Our traffic originates from the following IP ranges: `145.100.118.0/23` and `2001:610:9000::/40`.

## What to do if our measurements cause inconvenience?

We are committed to responsible network measurement practices to minimize the impact on infrastructure. If you believe our traffic is negatively affecting your systems, please contact us at tangled@utwente.nl so that we can work to resolve the problem. When reaching out to us, please provide the following information:

1. Your organization's name and a point of contact (name and email adddress).
2. The IP address(es) or prefixes from which you are receiving problematic traffic.
3. A description of the impact, including details such as the number of queries per second and their effects.
4. The date and time when you first observed problems that may be related to our measurements.

## Blocking our traffic

If you determine that it is necessary to block our traffic, we kindly request that you notify us so we can still exclude you from our measurements.

<div class="posts-list">
  {% for post in paginator.posts %}
  <article class="post-preview">
    <a href="{{ post.url | relative_url }}">
	  <h2 class="post-title">{{ post.title }}</h2>

	  {% if post.subtitle %}
	  <h3 class="post-subtitle">
	    {{ post.subtitle }}
	  </h3>
	  {% endif %}
    </a>

    <p class="post-meta">
      Posted on {{ post.date | date: "%B %-d, %Y" }}
    </p>

    <div class="post-entry-container">
      {% if post.image %}
      <div class="post-image">
        <a href="{{ post.url | relative_url }}">
          <img src="{{ post.image | relative_url }}">
        </a>
      </div>
      {% endif %}
      <div class="post-entry">
        {{ post.excerpt | strip_html | xml_escape | truncatewords: site.excerpt_length }}
        {% assign excerpt_word_count = post.excerpt | number_of_words %}
        {% if post.content != post.excerpt or excerpt_word_count > site.excerpt_length %}
          <a href="{{ post.url | relative_url }}" class="post-read-more">[Read&nbsp;More]</a>
        {% endif %}
      </div>
    </div>

    {% if post.tags.size > 0 %}
    <div class="blog-tags">
      Tags:
      {% if site.link-tags %}
      {% for tag in post.tags %}
      <a href="{{ '/tags' | relative_url }}#{{- tag -}}">{{- tag -}}</a>
      {% endfor %}
      {% else %}
        {{ post.tags | join: ", " }}
      {% endif %}
    </div>
    {% endif %}

   </article>
  {% endfor %}
</div>

{% if paginator.total_pages > 1 %}
<ul class="pager main-pager">
  {% if paginator.previous_page %}
  <li class="previous">
    <a href="{{ paginator.previous_page_path | relative_url }}">&larr; Newer Posts</a>
  </li>
  {% endif %}
  {% if paginator.next_page %}
  <li class="next">
    <a href="{{ paginator.next_page_path | relative_url }}">Older Posts &rarr;</a>
  </li>
  {% endif %}
</ul>
{% endif %}

