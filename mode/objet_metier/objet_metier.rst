


*************
Gestion des objets métiers
************* 

.. image:: ../../liste_objets_metier.png
 :scale: 50 %
 
   
1. Définition
***************** 
Un objet métier est une entié qui associe à un calque, les attributs d'une table de base de données. De la sorte, les attributs associés au calque sont affichables et éditables, dans le requêteur et dans le formulaire de création d'objet,  accessibles dans le mode Carte. 

Le mode Développement permet l'ajout, l'édition et la suppression d'objets métier. 


2. Création d'un objet métier
******************************************** 
La création d'un objet métier s'opère en deux temps : 

1.  La déclaration de l'objet et des paramètres d'affichage du requêteur.
2.  La construction des formulaires d'affichage, de création, d'édition et de recherche de l'objet métier via le studio. 


2.1. Déclaration d'un objet métier 
+++++++++++++++++++++++++++++
.. image:: ../../creation_objet_metier.png
 :scale: 80 %

Renseigner les champs suivants : 

* Titre: nom de l'objet métier tel qu'il apparaîtra dans le requêteur et dans le formulaire de création d'objet

 
.. image:: ../../lampe_requeteur.png
   :align: center
   :alt: Titre de l'objet tel qu'il apparaît dans le requêteur

.. image:: ../../lampe_creation.png
   :scale: 50 %
   :align: center
   :alt: Titre de l'objet tel qu'il apparaît dans le formulaire de création d'objet

* Champs id :  champ identifiant de la table. 
   
* Base de données : nom de la base de données à laquelle se connecter
   
* Schéma : schéma de la base de données 
   
* Table : table de la base de données 

* SQL Summary : requête SQL pour définir les champs à afficher dans l'infobulle d'un objet : 

.. image:: ../../infobulle.png

* SQL List : requête SQL pour définir les champs à afficher dans la liste des objets sélectionnés dun requêteur : 

.. image:: ../../liste_requeteur.png



2.2. Construction des formulaires d'un objet métier 
++++++++++++++++++++++++++++++++++++++++++++

 4 formulaires sont paramétrables : 
 
 1. Formulaire d'affichage de l'objet métier 
 2. Formulaire de recherche de l'objet métier 
 3. Formulaire de mise à jour de l'objet métier 
 4. Formulaire de création de l'objet métier 
 

