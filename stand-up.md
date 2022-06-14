---
name: stand-up
layout: page
permalink: /stand-up/
sitemap: false
---


<div id="users">
 <input class="search" placeholder="Search" />
 
 <br>

 <button class="sort" data-sort="name">Name</button>
 <button class="sort" data-sort="country">Country</button>
<br>
<br>
  <table>
    <!-- IMPORTANT, class="list" have to be at tbody -->
    <tbody class="list">
<tr>
  <td class="name">James Acaster</td>
  <td class="country">UK</td>
</tr>
<tr>
  <td class="name">Danielle Walker</td>
  <td class="country">Australia</td>
</tr>
<tr>
  <td class="name">Sam Campbell</td>
  <td class="country">Australia</td>
</tr>
<tr>
  <td class="name">Aaron Chen</td>
  <td class="country">Australia</td>
</tr>
<tr>
  <td class="name">Hanna Gadsby</td>
  <td class="country">Australia</td>
</tr>

    </tbody>
  </table>

</div>
<script src="//cdnjs.cloudflare.com/ajax/libs/list.js/1.5.0/list.min.js">



</script>

<script>
var options = {
  valueNames: [ 'name', 'country' ]
};

var userList = new List('users', options);

</script>


