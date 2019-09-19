# HubSpot-Blog

Template used by SimTalkBlog, using the HubSpot CMS platform.

## Project file structure

`simtalk-blog-2019.html` is the HTML template with HubL variables.\
`search-results-module.html` is the HTML system's page for search results.\
`about.html` is the about SimTalk Blog about HTML page.\
`assets/css/fontawesome-all.css` is Font Awesome's icons package.\
`assets/css/hubspot.css` is used for styling HubSpot modules and additional markup.\
`assets/css/main.css` is for general styling of the HTML template.\

## simtalk-blog-2019.html variables & code blocks

Linking CSS with HubL, replace `('/Dev/Blog Future Design/*)` with desired stylesheets 

``
    <link rel="stylesheet" href="{{ get_public_template_url('/Dev/Blog Future Design/assets/css/fontawesome-all.css') }}">
    <link rel="stylesheet" href="{{ get_public_template_url('/Dev/Blog Future Design/assets/css/main.css') }}">
    <link rel="stylesheet" href="{{ get_public_template_url('/Dev/Blog Future Design/assets/css/hubspot.css') }}">   
``

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
