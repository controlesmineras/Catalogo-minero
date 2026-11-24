---
title: Fichas de elementos
---
# Fichas de elementos

{% assign fichas = site.pages | where: "layout", "ficha" | sort: "title" %}
<ul id="fichas">
{% for ficha in fichas %}
  <li><a href="{{ ficha.url | relative_url }}" data-foto="{{ ficha.foto | escape }}" data-anteriores="{{ ficha.fotos_anteriores | join: '|' | escape }}">{{ ficha.title | escape }}</a></li>
{% endfor %}
</ul>

<script>
const foto = new URLSearchParams(location.search).get('foto');
if (foto && /^[\w.-]+\.(?:jpe?g|png|webp)$/i.test(foto)) {
  const ficha = Array.from(document.querySelectorAll('#fichas a')).find(link =>
    link.dataset.foto === foto || link.dataset.anteriores.split('|').includes(foto)
  );
  location.replace(ficha ? ficha.href : './' + encodeURIComponent(foto));
}
</script>
