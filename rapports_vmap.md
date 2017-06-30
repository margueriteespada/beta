# Rapports objets métiers

![Liste des rapports](liste_rapports_objets_metier.png)

## 1. Définition
Un rapport sur objet métier permettra à l'utilisateur de générer des fichiers .pdf ou .doc sur des informations d'un objet sélectionné dans le panier.
Il y a différents types de rapports: 

 - Les rapports sur un élément ![logo rapport simple](logo_rapport_simple.png)
 - Les rapports sur plusieurs éléments ![logo rapport multi](logo_rapport_multi.png)

Si un utilisateur sélectionne plusieurs entités et lance un rapport sur un élément, alors plusieurs fichiers seront générés, à contrario si il lance un rapport sur plusieurs éléments, un seul fichier contenant les informations de chacun des éléments sera généré.

![Exemple de rapport vMap en pdf](exemple_rapport_pdf.png)

## 2. Utilisation
Pour générer un rapport sur objet métier, il suffit de sélectionner un objet sur la carte en cliquant dessus, de l'ajouter au panier, puis sélectionner les objets qui vous intéressent dans le panier et enfin à l'aide du bouton "Rapports" générer le rapport voulu.

![creation_rapport_vmap](creation_rapport_vmap.png)

## 3. Administration
Dans l'interface d'administration nous distinguons les éléments suivants:

 - Nom: le nom qui sera affiché dans l'interface
 - Format d'impression: A4/A3
 - Orientation: portrait/paysage
 - Format de sortie: pdf/doc
 - Objet métier: objet métier sur lequel le rapport est disponible
 - Rapport sur plusieurs éléments: pour générer un ou plusieurs documents en cas de multiple sélection
 - Définition HTML: permet de configurer la mise en page
 - Objets JSON: permet une configuration plus avancée

![administration_rapports](administration_rapports.png)

### 3.1. Configuration de la définition HTML
Dans cette partie vous allez configurer la mise en page de votre rapport, pour cela il est conceillé d'avoir trois parties:

 - le style: une balise style qui contiendra la définition CSS à utiliser.
 - le corps: des balises HTML permettant de faire la mise en page.
 - le script: une balise script qui lancera du JavaScript lors de la génération (cela permettra de gérer les sauts de page par exemple).

#### 3.1.1. Utilisation des variables
Dans le corps vous aurez accès à la librairie AngularJS, c'est à dire que vous pouvez utiliser la syntaxe suivante pour afficher le contenu d'une variable:
```html
<label class="fichelabel">Nom: {{BO.nom}}</label>
```
Sur l'exemple ci-dessus vous aurez peut être constaté la présence de la variable BO, celle-ci est présente par défaut et contient les attributs de l'objet résultant (notez que pour un rapport à plusieurs éléments elle se composera d'un tableau contenant les divers objets retournés).

Avec la librairie AngularJS vous pouvez facilement effectuer des boucles, des conditions, des changements de style etc.. 

Voici un exemple permettant de faire une boucle et lister les lampes d'une route
```html
<!--Description des lampes de la route-->
<div ng-repeat="oLampe in aLampes" ng-if="oLampe.lampe_id!=undefined" class="description_box border_container">
	<label class="fiche_label">Lampe: {{oLampe.nom}}</label>
	<label class="fiche_label">Id: {{oLampe.lampe_id}}</label>
	<label class="fiche_label">Puissance: {{oLampe.puissance}}</label>
	<label class="fiche_label">Allumée: {{oLampe.allume ? 'Oui' : 'Non'}}</label>
</div>
```

#### 3.1.2. Affichage de la carte
Si vous voulez afficher une ou plusieurs cartes dans votre rapport, vous devrez dans une première partie créer une balise image avec un "id" de votre choix (il est conseillé d'utiliser un fond transparent au cas où les tuiles ne se chargent pas lors de l'impression):
```html
<img id="map_image" src="images/transparent.png">
```
La seconde partie de la manipulation consiste à paramétrer un objet JSON pour dire à vMap quelle carte il doit utiliser et de quelle façon, pour cela veuillez vous référer à la partie [3.2.1. Configuration des cartes à utiliser dans le template HTML](#3.2.1-configuration-des-cartes-a-utiliser-dans-le-template-html)

### 3.2. Configuration des objets JSON
Pour bien configurer son rapport il est utile de configurer la partie Objets JSON. Le but est de pouvoir ajouter des cartes au rapport, interroger des webservices ou afficher des images.
Pour cela il faudra créer en JSON un tableau contenant les différentes configurations, et chacune de ces configurations sera typée avec l'argument "type".

Exemple:
```json
[{
	"type":"map",
	"target":"#map_image",
	"map_id":120,
	"resolution_coeff":1,
	"scale_target":"map_scale"
}, {
	"type":"webservice",
	"ressource":"vitis/genericquerys",
	"params":{
		"schema":"sig",
		"table":"lampe",
		"filter":"{\"column\":\"route_id\", \"compare_operator\":\"=\", \"value\": \"{{BO.route_id}}\"}"
	},
	"target": "aLampes"
}, {
	"type":"object",
	"content":{
		"company":"Veremes"
	},
	"target": "scope"
}]
```

#### 3.2.1 Configuration des cartes à utiliser dans le template HTML
Vous pouvez inclure des cartes dans vos formulaires en utilisant des objets de type "map" avec les paramètres suivants:

 - target: cible sur laquelle doit se poser la carte ("#" + l'identifiant de votre balise image)
 - map_id: l'identifiant de la carte à utiliser
 - resolution_coeff: coefficient de résolution
 - scale_target: nom de la variable qui contiendra l'échelle de la carte dans le template HTML

Exemple: 
```json
{
	"type":"map",
	"target":"#map_image",
	"map_id":120,
	"resolution_coeff":1,
	"scale_target":"map_scale"
}
```
Ici on vient afficher le(s) objets métier sur la carte 120 dans la balise image "#map_image" tout en mettant son échelle dans la variable "map_scale".

#### 3.2.2. Configuration des webservices 
Vous pouvez demander à effectuer des requêtes vers des webservices vMap (PHP) pour afficher le résultat dans la vue HTML au travers de variables que vous nommerez.
Pour cela il faudra utiliser le type "webservice" et utiliser les paramètres suivants:

 - ressource: la ressource à interroger
 - params: les paramètres à utiliser lors de l'interrogation
 - target: ne nom de la variable créee qui contiendra les informations retournées

Important: vous pouvez tout comme dans la Définition HTML utiliser des doubles accolades pour utiliser une variable BO.

Exemple: 
```json
{
	"type":"webservice",
	"ressource":"vitis/genericquerys",
	"params":{
		"schema":"sig",
		"table":"lampe",
		"filter":"{\"column\":\"route_id\", \"compare_operator\":\"=\", \"value\": \"{{BO.route_id}}\"}"
	},
	"target": "aLampes"
}
```
Ici on fait une requête au webservice vitis/genericquerys qui permet d'interroger de façon générique des tables. 
Avec cet appel et en utilisant les doubles accolades {{BO.route_id}}, je peux afficher l'ensemble des lampes contenues dans ma route.

#### 3.2.2. Configuration des images
Vous pouvez afficher des images pré-définies en utilisant le type image et les paramètres suivants:

 - imageUrl: URL de l'image (peut être une définition base-64)
 - target: cible sur laquelle doit se poser l'image ("#" + l'identifiant de votre balise image)

Exemple: 
```json
{
	"type":"image",
	"imageUrl":"data:image/png;base64,iVBORw0KGgoAAAANSUh...",
	"target":"#img1"
}
```
