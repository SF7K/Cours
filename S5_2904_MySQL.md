Liste des fonctions ineternes à PHP :  

https://www.php.net/manual/fr/indexes.functions.php  


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
);  

Exemple:  
CREATE TABLE ingredients (
-> id INT(100) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
-> name VARCHAR(255) NOT NULL,
-> weight  INT(100),
-> price FLOAT(23) NOT NULL,
-> calorie FLOAT(23)
);

############################  

# Insérer des données dans une table  
INSERT INTO <nom_de_la_table> (colonne N°1, colonne N°2, colonne N°3, etc...)  
VALUES (valeur N°1, valeur N°2, valeur N°3, etc...)  

Exemple:  
INSERT INTO ingredients (name, weight, price, calorie)   
VALUES ("cheese", 20, 35, 100);  

Objectif:   

1) Créez 2 ingrédients qui possèdent une même valeur commune (le prix, le poids ou les calories)  
2) Trouvez la requête qui permet d afficher uniquement ces deux ingrédients. Pour ce faire, vous devrez SELECT ces ingrédients en spécifiant ne vouloir choisir que les
ingrédients dont le poids est = à 30  
Exemple:   

| id | name   | weight | price | calorie |  
+----+--------+--------+-------+---------+   
|  1 | cheese |     20 |    35 |     100 |  
|  2 | bacon  |     20 |    35 |    1000 |  
|  3 | salad  |   2044 |   350 |     100 |  

Requête qui permet d afficher tous les produits dont calorie est == 100  

RTFM = Read The Fucking Manual ====> Google est ton ami :>  
