Liste des fonctions ineternes à PHP :  

https://www.php.net/manual/fr/indexes.functions.php  

###
########################################################  
Partie MySQL  
                 ᕕ( ᐛ )ᕗ  
########################################################   

Se connecter sur son MySQL: mysql -u<nom_du_user> -p<password_du_user>  
Voir les databases: show databases;  
Utiliser une DB en particulier: use <nom_de_la_DB>;  
Afficher les tables de la DB: show tables;  

Voir ce qu'il y a à l'intérieur d'une table: describe <nom_de_la_table>;  

Créer une DB: create database <nomDB>        =========> Le nom de la DB doit être en minuscule (et/ou camelCase) et au singulier  
Créer une table: tabletable  

CREATE TABLE <nom_de_la_table> (             ==========> Le nom des tables doit toujours être en minuscule ET au pluriel  
<nom_colonne> <type> <infos>,  
<nom_colonne> <type> <infos>,  
<nom_colonne> <type> <infos>,  
<nom_colonne> <type> <infos>,  
<nom_colonne> <type> <infos>,  
<nom_colonne> <type> <infos>  
)  
