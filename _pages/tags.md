---
layout: default
title: Štítky
permalink: /tags/
---

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %} {% assign
tag_words = site_tags | split:',' | sort %}

<!-- begin tags -->
<section class="tags">
	{% for item in (0..site.tags.size) %}{% unless forloop.last %} {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}

	<div class="tags__inner is-hidden" id="{{ this_word | cgi_escape }}">
		<div class="container">
			<div class="row">
				<div class="col col-12">
					<div class="tag__info">
						{% for post in site.tags[this_word] limit:1 %} {% if post.image != null %}
						<div class="tag__image">
							<img class="lazy" data-src="{{site.baseurl}}{{post.image}}" alt="{{this_word | capitalize}}" />
						</div>
						{% endif %} {% endfor %}
						<h2 class="tag__name">{{ this_word }}</h2>
						<div class="tag__counter">
							{{ site.tags[this_word].size }} {% if site.tags[page.tag].size < 2 %}příspěvek{% else if site.tags[page.tag].size < 5
							%}příspěvky{% else %}příspěvků{% endif %}
						</div>
					</div>
				</div>
			</div>
		</div>

		<div class="container animate">
			<div class="row">
				{% for post in site.tags[this_word] %} {% if post.title != null %} {% include article.html %} {% endif %} {% endfor %}
			</div>
		</div>
	</div>

	{% endunless %} {% endfor %}
</section>
<!-- end tags -->

<script>
	var tag_name = window.location.search.replace("?tag=", "#");
	if (tag_name) {
		var el = document.querySelector(tag_name);
		el.classList.remove("is-hidden");
	}
</script>