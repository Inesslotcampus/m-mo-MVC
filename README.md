# memo-MVC

__MVC ( modèle-vu-controleur) =motif architecture logicielle déstiné aux interfaces graphiques très populaire pour appli web. Permet d'organiser son code source. Permet de savoir quel fichier créer et leurs rôles. Utilisé dans bcp de frameworks
Sépare la logique du code en 3 parties:__

- Modèle(Model) = données à afficher. Récupère infos brutes dans la bdd et les organise ,rassemble pr être traitées par le contrôleur. On y retrouve uniquement les requêtes sql. 

- vue (view) = présentation de l'interface graphique (concentre sur l'affichage) Récupère les variables pour savoir ce qu'elles affichent. composé essentiellement du code HTML, peut aussi avoir boucles et conditions PHP très simples.

- controleur (controller) = logique contenant des actions efféctuées par l'utilisateur. Intermédiaire entre le modèle et la vue. Demande au modèle d'analyser, prendre des décisions et renvoyer le txt à afficher à la vue. Contient principalement du php. Détermine si visiteur a le droit de voir la page ou pas. Il reçoit la requête du visiteur et contacte modèle et vu pour échanger infos.

## Le routeur

__Dans MVC seul fichier qui est le point d'entrée de l'application, quelle que soit la page affichée. Systématiquement appelé, envoie la demande au bonc controleur. Trouve le bon chemin pour que l'utilisateur récupère la bonne page. fichier index.php qui est à la racine publique de notre projet.__

//http://url_du_site/controleur/methode//

### .htacces

__réécriture d'URL proposé par les serveurs Apache avec fichier .H=htacces__

//RewriteEngine On // permet de démarer la réécriture d'Url
//RewriteRule ^([a-zA-Z0-9\-\_\/]*)$ index.php?p=$1//  permet de définir une règle de réécriture d'URL
([a-zA-Z0-9\-\_\/]* = diff caractères pris en compte dans URL pour sa réécriture 

ex url finale: http://url_du_site/index.php?p=articles/lire

### index.php

__Contient données Url.__ 
1. Appeler ds fichier, controleur et modèle principaux qui servent de base commune à tous les fichiers.
2. Pour la protabilité du projet: sauvegarder chemin généré dans la constante "ROOT"
3. Constante géréré depuis des infos dans la super globale "$_SERVER" qui contient le chemin complet vers notre fichier
4. Enlever nom "index.php" au moyen de la fonction php "str_replace" // define('ROOT', str_replace('index.php','',$_SERVER['SCRIPT_FILENAME']));//
5. on peut utiliser root pour appeler nos fichiers //require_once(ROOT.'app/Model.php');
require_once(ROOT.'app/Controller.php');//

## paramètres d'URL

__Bout de code qui permet au routeur de lire une URL:__
// On sépare les paramètres et on les met dans le tableau $params
$params = explode('/', $_GET['p']);

// Si au moins 1 paramètre existe
if($params[0] != ""){
    // On sauvegarde le 1er paramètre dans $controller en mettant sa 1ère lettre en majuscule
    $controller = ucfirst($params[0]);

    // On sauvegarde le 2ème paramètre dans $action si il existe, sinon index
    $action = isset($params[1]) ? $params[1] : 'index';

}else{
    // Ici aucun paramètre n'est défini
}



