# Linux
## Lignes de commande
  *ouverture avec CTRL+ALT+T*
  * cd : Change Directory ( ~ User) ( / Racine)
  * ls : Liste des fichiers/dossier (dans le répertoire)
  * cd ../ : Revenir un pas en arrière (ajouté ../ rajoute un pas)
  * clear : nettoie la fenêtre MAIS les lignes restent en haut
  * cp : copier un fichier/dossier (cp home/user/file.fi home/directory)
  * mv : déplacer un fichier/dossier (cp home/user/file.fi home/directory)
  * rm : remove fichier/dossier
  * nano : éditer ou créer un fichier
  * mkdir : créer un dossier
  * touch : créer un fichier
  * sudo : Super User do
  * update : check les versions disponibles
  * upgrade : installes les M.A.J. trouvées lors de l'update
  * install : installe une application
  * service : pour agir sur des services
  * apt : pour agir sur des paquets
  * grep : recherche d'info *ex d'utilisation : sudo service apache 2 status | grep "Active"* **ne pas oublier le pipe !**


**Fonctions / Argument :**
  * -r : recursive - remove directory & content
  * -f : forcer l'action
  * -d : delete les dossiers vides
  * -rf : on supprime dossier/fichier sans demander validation

## Script
  * echo "texte" : écrit "texte" dans la console
  * read : permet à l'utilisateur d'entrer des caractères
  * $input : prends la valeur de l'input
**Conditions**
*si une condition est vraie la boucle se finie, elle ne vérifie pas les autres conditions.*
  * Si : if [ $input=X ] fermer la condition par une ligne "fi"
  * Alors : then echo "text" (par exemple)
  * Sinon si : elif [ $input=X ]
  * Tant que : while [[ $input != '']] (tant que l'input est différent de "vide")
  * do : Fais/Execute *si do est engagé en condition, il faudra terminer par done*
  * && : et *si un && est engagé dans une condition, il faudra utiliser des doubles crochets [[ ]]*
  * || : ou *si un || est engagé dans une condition, il faudra utiliser des doubles crochets [[ ]]*

**Fonctions / Arguments**
  * -lt : Lesser Than (plus petit que <)
  * -le : Lesser or Equal (plus petit ou égale à =<)
  * -gt : Greater Than (plus grand que >)
  * -ge : Greater or Equal (plus grand ou égal à =>)
---
*exemple : calculatrice*
1. #!/bin/bash  
2.
3. **echo "Entrée 1 :"**  
4. *read input1*  
5. **echo "Opérateur :"**  
6. *read operator*  
7. **echo "Entrée 2 :"**  
8. *read input2*  
9. ***total=$(($input1$ operator $input2))***  
10. **echo "Total" $total**  
---
*exemple : trouver un nombre random, avec répétition de demande*

1. #!/bin/bash  
2.
3. reponse=$(((RANDOM % 100) +1))  
4. *while [[ $input != $reponse ]]; do*  
5.  **echo "Entre un nombre entre 10 et 100"**  
6. read input  
7.
8. clear  
9.
10. *if [ $input = '12' ]; then*  
11.  **echo "C'est juste, 12 est toujours la réponse."**  
12. *elif [ $input -gt 100 ]; then*  
13.  **echo "On a dit entre 10 et 100 ducon !"**  
14. *elif [ $input -lt 10 ]; then*  
15.  **echo "On a dit entre 10 et 100 ducon !"**  
16. *elif [ $input = $reponse ]; then*  
17.  **echo "Bien joué frer !"**  
18. *elif [ $input -lt $reponse ]; then*  
19.  **echo "C'est plus, essaie encore !"**  
20. *elif [ $input -gt $reponse ]; then*  
21.  **echo "C'est moins, essaie encore !"**  
22. fi  
23. done  
---
*exemple d'utilisation des conditions OU || et ET &&*

1. #!/bin/bash  
2. *while [[ $input1 = '' ]]; do*  
3. clear  
4. **echo "Entrée 1 :"**  
5. read input1  
6. done  
7. *while ! [[ $operator = '+' || $operator = '-' || $operator = '* * *' || $operator = '/' ]]; do*  
8. clear  
9. **echo "Opérateur"**  
10. read operator  
11. done  
12. *while [[ $input2 = '' ]]; do*  
13. clear  
14. **echo "Entrée 2 :"**  
15. read input2  
16. *done*  
---
*utilisation des fonctions*
#!/bin/bash
clear

function start() {
    clear
    vagrant global-status
    echo ''
    echo 'Quel VM voulez-vous allumer?'
    read -p 'id :' id
    vagrant up $id
    menu
}

function stop() {
    clear
    vagrant global-status
    echo ''
    echo 'Quel VM voulez-vous arrêter?'
    read -p 'id :' id
    vagrant halt $id
    menu
}

function destroy() {
    clear
    vagrant global-status
    echo ''
    echo 'Quel VM voulez-vous supprimer?'
    read -p 'id :' id
    vagrant destroy -f $id
    vagrant remove $id
    menu
}

function menu() {
    echo "********************************"
    echo "*                              *"
    echo "*         Scriptomania         *"
    echo "*                              *"
    echo "********************************"
    echo ""
    echo ""
    vagrant global-status --prune
    echo "Que voulez-vous faire?"
    sleep 1
    echo "1. Allumer une vm"
    echo "2. Eteindre une vm"
    echo "3. Supprimer une vm"
    read choice

    if ! [ $choice = 1 && $choice = 2 && $choice = 3 ]; then
        read choice
    elif [ $choice = 1 ]; then
        start
    elif [ $choice = 2 ]; then
        stop
    elif [ $choice = 3 ]; then
        destroy
    fi
}

menu
