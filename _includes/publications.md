<h2 id="publications" style="margin: 2px 0px -15px;">Publications</h2>

<div class="publications">
<ol class="bibliography">

{% for link in site.data.publications.main %}

<li{% if forloop.index > 5 %} class="extra-pub"{% endif %}>
<div class="pub-row">
  <div class="col-sm-3 abbr" style="position: relative;padding-right: 15px;padding-left: 15px;">
    {% if link.image %} 
    <img src="{{ link.image }}" class="teaser img-fluid z-depth-1" style="width=100%;height=40%">
    {% if link.conference_short %} 
    <abbr class="badge">{{ link.conference_short }}</abbr>
    {% endif %}
    {% endif %}
  </div>
  <div class="col-sm-9" style="position: relative;padding-right: 15px;padding-left: 20px;">
      <div class="title"><a href="{{ link.pdf }}">{{ link.title }}</a></div>
      <div class="author">
        {% assign processed_authors = link.authors %}
        {% for author_pair in site.data.authors %}
          {% assign author_name = author_pair[0] %}
          {% assign author_url = author_pair[1] %}
          {% assign linked_author = '<a href="' | append: author_url | append: '" target="_blank">' | append: author_name | append: '</a>' %}
          {% assign processed_authors = processed_authors | replace: author_name, linked_author %}
        {% endfor %}
        {{ processed_authors }}
      </div>
      <div class="periodical"><em>{{ link.conference }}</em>
      </div>
    <div class="links">
      {% if link.pdf %} 
      <a href="{{ link.pdf }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">PDF</a>
      {% endif %}
      {% if link.code %} 
      <a href="{{ link.code }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">Code</a>
      {% endif %}
      {% if link.page %} 
      <a href="{{ link.page }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">Project Page</a>
      {% endif %}
      {% if link.bibtex %} 
      <a href="{{ link.bibtex }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">BibTex</a>
      {% endif %}
      {% if link.notes %} 
      <strong> <i style="color:#e74d3c">{{ link.notes }}</i></strong>
      {% endif %}
      {% if link.others %} 
      {{ link.others }}
      {% endif %}
    </div>
  </div>
</div>
<br>
</li>

{% endfor %}

</ol>

{% assign total_pubs = site.data.publications.main | size %}
{% if total_pubs > 5 %}
{% assign hidden_count = total_pubs | minus: 5 %}
<div class="toggle-pubs-wrap">
  <button type="button" id="toggle-pubs" onclick="togglePublications()">View earlier work &#9662;</button>
</div>
<script>
function togglePublications() {
  var container = document.querySelector('.publications');
  var btn = document.getElementById('toggle-pubs');
  var expanded = container.classList.toggle('expanded');
  btn.innerHTML = expanded ? 'Show less &#9652;' : 'View earlier work &#9662;';
}
</script>
{% endif %}
</div>
