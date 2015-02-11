# Formulaire-Javascript-Css3
formulaire avec affichage dynamique

## Mon Site  Web : http://creative-designer-builder.fr/



Vous trouverez ici un formulaire de recherche sous javascript

## Rendu

<http://codepen.io/Busuttil-Nicolas/pen/xbpOPW>


##Code Javascript base

On initialise tout d'abord l'input avec l'évent <strong>Keypress</strong> (pour plus d'information : <http://api.jquery.com/keyup/> )

```shell
$('input').on('keyup', function () {
    var valProduit = $('#produit').val();
    var dataProduit = (valProduit == '') ? '' : '[data-produit="' + valProduit + '"]';

    $(".card").hide();
    $("div" + dataProduit).show();
});
```
Exécution du JS uniquement lorsque la page est prête (document ready)
```shell
$(function() {
    $('input').on('keyup', function () {
        var valProduit = $('#produit').val();
        var dataProduit = (valProduit == '') ? '' : '[data-produit="' + valProduit + '"]';

        $(".card").hide();
        $("div" + dataProduit).show();
    });
});
```

Recherche floue : on utilise *= dans le sélecteur CSS, et on cible la class qu'on veut cacher, car le choix des divs est trop large.
```shell
$(function() {
    $('input').on('keyup', function () {
        var valProduit = $('#produit').val();
        //rajout de *= à data-produit pour qu'il récupère soit la fin soit le début d'un mot.
        var dataProduit = (valProduit == '') ? '' : '[data-produit*="' + valProduit.toLowerCase() + '"]';

        $('.card:not(.card' + dataProduit + ')').hide();
        $(".card" + dataProduit).show();
    });
});
```

Ajout d'un délai sur le traitement de la recherche
```shell
$(function() {
  var delay;
  $('#produit').on('keyup', function() {
    if(delay){
      clearTimeout(delay);
    }
    
    delay = setTimeout(function() {
      var valProduit = $('#produit').val();
      var dataProduit = (valProduit == '') ? '' : '[data-produit*="' + valProduit.toLowerCase() + '"]';
      
      $('.card:not(.card' + dataProduit + ')').hide();
      $(".card" + dataProduit).show();
      }, 100);
    });
  });
```
On exécute le sélecteur CSS une seule fois <strong>#produit</strong> et <strong>#card</strong> & rajout d'une transition de début et de fin, grâce au if, else

```shell
$(function() {
    var delay,
        produit =  $('#produit'),
        cards = $('.card');

    produit.on('keyup', function() {
        if (delay) {
            clearTimeout(delay);
        }

        delay = setTimeout(function() {
            var valProduit = produit.val();
            var dataProduit = (valProduit == '') ? '' : '[data-produit*="' + valProduit.toLowerCase() + '"]';

            if (valProduit) {
                cards.not('.card' + dataProduit).fadeOut();
                cards.filter(dataProduit).fadeIn()
            } else {
                cards.fadeIn();
            }
        }, 10);
    });
});
```
Pour plus d'information sur <strong>fadeOut()</strong> et <strong>fadeIn()</strong>
* <http://api.jquery.com/fadein/>
* <http://api.jquery.com/fadeout/>
