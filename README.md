# HubSpot-Blog

Template used by SimTalkBlog, developed using the HubSpot CMS platform.

## Project file structure

`simtalk-blog-2019.html` is the HTML template with HubL variables.\
`search-results-module.html` is the HTML system's page for search results.\
`about.html` is the about SimTalk Blog about HTML page.\
`assets/css/fontawesome-all.css` is Font Awesome's icons package.\
`assets/css/hubspot.css` is used for styling HubSpot modules and additional markup.\
`assets/css/main.css` is for general styling of the HTML template.\

## simtalk-blog-2019.html variables & code blocks

Blog's title/name: `{{ content.html_title }}`

Blog's meta description: `{{ content.meta_description }}`

HubSpot's obligatory header includes: `{{ standard_header_includes }}`

Linking CSS with HubL, replace `('/Dev/Blog Future Design/*)` with desired stylesheets 

`<link rel="stylesheet" href="{{ get_public_template_url('/Dev/Blog Future Design/assets/css/fontawesome-all.css') }}">`

Blog's root directory URL: `{{ group.absolute_url }}` 

Search bar HubSpot module:

``
<div class="hs-search-field"> 
  <div class="hs-search-field__bar"> 
    <form action="/{{ site_settings.content_search_results_page_path }}">
      {% if module.field_label %}
        <label for="term">{{ module.field_label }}</label>
      {% endif %}
      <input style="background-color: #fff;" type="text" class="hs-search-field__input" name="term" autocomplete="off" aria-label="{{ module.field_label || "Search" }}" placeholder="Search for a post...">
      {% if module.content_types.website_pages %}
        <input type="hidden" name="type" value="SITE_PAGE">
      {% endif %}
      {% if module.content_types.landing_pages %}
        <input type="hidden" name="type" value="LANDING_PAGE">
      {% endif %}
      {% if module.content_types.blog_posts %}
        <input type="hidden" name="type" value="BLOG_POST">
        <input type="hidden" name="type" value="LISTING_PAGE">
      {% endif %}
      {% if module.content_types.knowledge_articles %}
        <input type="hidden" name="type" value="KNOWLEDGE_ARTICLE">
      {% endif %}

      {% if module.include_search_button %}
        <button aria-label="Search">{% icon name="search" style="solid" %}</button>
      {% endif %}
    </form>
  </div>
  <ul class="hs-search-field__suggestions"></ul>
</div>
``              

Standard HubSpot blog content areas are created with a master if statement that evaluates whether the user is looking at a listing or a individual post. `{% if is_listing_view %}` checks if it is a listing, otherwise it will render the HTML for a post.\

The listing of posts is generated by a for loop that iterates through your blog posts and lists the posts based on the user's request. The for loop iterates through "content in contents". Contents is a predefined sequence of content that contains all the posts contained in that blog. Example: `{% for post in contents %}`

### Post variables

- `{{ post.absolute_url }}` = URL of a single post.
- `{{ post.name }}` = A string containing the post's title.
- `{{ post.publish_date|datetimeformat('%B %e, %Y') }}` = The date the post was published.
- `{{ group.absolute_url}}/author/{{ post.blog_post_author.slug }}` = Post author's URL.
- `{{ post.blog_post_author.display_name |truncate(25) }}` = Post author's name. (limited to 25 characters max)
- `{{ post.blog_author.avatar }}` = Post author's avatar.
- `{{ post.featured_image }}` = Post's featured image.
- `{{ post.post_summary |truncate(360) }}` = Post's summary string. (limited to 360 characters max).

### Post stats and misc

 `{% for topic in post.topic_list %}` Renders a list of the topics added to the post, linked to the respective topic listing page. 
