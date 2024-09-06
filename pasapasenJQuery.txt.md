En Jquery
Voici une solution en Jquery, simple à mettre en place. Jquery c'est une bibliothèque JavaScript qui permet de faire pleins de choses en JS plus "facilement". Mais il faut aussi apprendre à l'écrire. Nous ici on va juste se contenter de recopier le code et de le comprendre.

Ajouter cette balise scripts à votre <head> pour inclure Jquerry à chacune de vos pages (index/discover/comments).

<script src="https://code.jquery.com/jquery-3.5.1.js" integrity="sha256-QWo7LDvxbWT2tbbQ97B53yJnYU3WhH/C8ycbRAkjPDc=" crossorigin="anonymous"></script>
Créez une page script.jset ajoutez ce bout de code.

$(function(){
  $("#header").load("../components/header.html"); 
  $("#footer").load("../components/footer.html"); 
});
💡 Comme nous utilisons LiveServer pour tester nos pages, on peut mettre dans nos chemins "../" pour toujours revenir à la racine de notre site pour chercher après nos composants. Car si on ne le fait pas, les chemins seront différents si on est sur "index.html" qui est censé être à la racine et les autres pages qui sont dans un dossier "pages"

❗ Attention, regarder bien le chemin vers le header/footer et ajuster vos fichiers en fonction.

❗NPO: ajouter la ligne qui permet d'inclure votre page script à chacune de vos pages.

<script src="script.js"></script>
Ensuite on va ajouter nos ID définit plus haut à chacune de nos balises header et footer sur chacune de nos pages(index/discover/comments) pour définir l'endroit où le contenu de vos pages header et footer apparaîtront.

<header id="header"></header>
<footer id="footer"></footer>
Vous pouvez maintenant créer une page header.html et footer.html, les placées dans un dossier "components" et elles seront ajoutées dans les balises header et footer.

Changer le style du menu (optionnel)
Si vous souhaitez changer le style du lien dans le menu en fonction de la page sur laquelle vous êtes, il va falloir de nouveau "hacker" le système un tout petit peu.

On va de nouveau utiliser un peu de JQuery pour parvenir à nos fins.

Créez une nouvelle page nav.jset copiez le code suivant:

$('nav a').each(function() {
  if ($(this).attr('href') == location.href.split("/").slice(-1)){ $(this).addClass('isActive'); }
});
Ce code va sélectionner toutes nos balises <a> contenue dans notre balise <nav>. Donc ayez une navigation dans votre header qui fonctionne avec ce principe, ou alors changer la partie du script pour qu'elle corresponde à ce que vous avez vous. Ensuite le script va comparer le nom du fichier dans l'attribut hrefet le comparer au nom du fichier dans l'adresse du navigateur (sans le .html), si il y a une correspondance il va ajouter une classe 'isActive` à ce lien.

<nav>
  <a href="discover.html">Discover</a>
  <a href="comments.html">Comments</a>
</nav>
Il reste à créer une classe CSS isActive avec les propriétés voulue et le tour est joué.

.isActive{
  background-color: red;
}
❗ N'oubliez pas de lier votre nouvelle page nav.js dans votre header.html!

Variante bonus (optionnel)
Si vous voulez une propriété différente pour chacun de vos liens, vous pouvez employez ce code Jquery.

let fileName = location.href.replace(/\.[^/.]+$/, "").split("/").slice(-1);
$('nav a').each(function() {
  if ($(this).attr('href') == location.href.split("/").slice(-1)){ $(this).addClass(fileName); }
});
Ensuite il faudra un sélecteur CSS pour chacun des noms de fichier que vous avez.

.fileName{
  font-size: 2em;
}
La différence ici c'est qu'il va ajouter une classe avec le même nom que le fichier. Du coup vous pouvez séparer vos styles pour chacun des liens du menu.