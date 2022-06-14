---
title: books
layout: page
permalink: /books/
sitemap: false
---


<div id="users">
 <input class="search" placeholder="Search" />
 
 <br>

 <button class="sort" data-sort="title">Título</button>
 <button class="sort" data-sort="year">Ano</button>
 <button class="sort" data-sort="author">Autor/a</button>
 <button class="sort" data-sort="country">País</button>
 <button class="sort" data-sort="publisher">Publisher</button>
<br>
<br>
  <table>
    <!-- IMPORTANT, class="list" have to be at tbody -->
    <tbody class="list">

<tr>
  <td class="title">Persuasion</td>
  <td class="year">1817</td>
  <td class="author">Austen, Jane</td>
  <td class="country">UK</td>
  <td class="publisher">Project Gutenberg</td>
</tr>
<tr>
  <td class="title">Pride and Prejudice</td>
  <td class="year">1813</td>
  <td class="author">Austen, Jane</td>
  <td class="country">UK</td>
  <td class="publisher">Project Gutenberg</td>
</tr>

    </tbody>
  </table>

</div>

<script src="{{ site.baseurl }}/list.min.js"></script>

<script>
var options = {
  valueNames: [ 'title', 'year', 'author', 'country', 'publisher', ]
};

var userList = new List('users', options);

</script>


