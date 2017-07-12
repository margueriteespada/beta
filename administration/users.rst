

Gestion des utilisateurs 
#########################

Un utilisateur vMap est un compte connu par l’application vMap qui peut se connecter et utiliser ses services. 

Deux profils d’utilisateurs sont à distinguer :

 * Utilisateurs PostgreSQL : utilisateurs authentifiés par la base de données interne à vmap, PostgreSQL, créés directement dans vMap. 
 
 * Utilisateurs Active Directory (AD) : utilisateurs d’un domaine et authentifiés par un annuaire Active Directory, importés dans vMap.
 
 
 
 
 
1. Création d'utilisateurs et de groupes PostgreSQL
************************************************************

Le mode ‘Utilisateurs > Onglet Utilisateurs’ liste l’ensemble des utilisateurs. Il permet l’ajout de nouveaux utilisateurs, leur édition et suppression. Après avoir cliqué sur ‘Ajouter un utilisateur’, le formulaire suivant s’affiche :

.. image:: ../images/vitis_formulaire_users.png
 :scale: 80 %



2. Création d'utilisateurs et de groupes d'un annuaire Active Directory
***********************************************************************

Il est possible de gérer plusieurs domaines et d’exploiter des groupes de sécurité définis directement dans un annuaire Active Directory. 
 
L’administrateur a la possibilité d’importer des utilisateurs et des groupes depuis Active Directory. Cette méthode permet d’hériter des droits issus de la gestion centralisée AD des utilisateurs au sein d’un organisme. 
 
L’administrateur crée  le nouveau domaine, puis importe les utilisateurs et les groupes. L’attribution des groupes ainsi que les mots de passe des utilisateurs ne pourront pas être changés.

2.1 Ajout de domaines Active Directory
----------------------------------------

Le mode ‘Utilisateurs> Onglet Domaines’ liste les domaines Active Directory. Il permet de créer, modifier et supprimer des domaines. Le bouton ‘Ajouter un Domaine’ affiche le formulaire suivant : 


 







