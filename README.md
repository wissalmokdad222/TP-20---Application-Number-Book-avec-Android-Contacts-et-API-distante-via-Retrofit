# Number Book - Application Android connectée

Cette application permet de lire les contacts d'un téléphone Android, de les afficher dans une liste et de les synchroniser avec une base de données distante MySQL via une API PHP.

## Étapes de réalisation

1.  **Base de données** : Création de la base `numberbook` et de la table `contact` pour stocker les noms et numéros.
2.  **Backend PHP** : Développement d'une API REST simple pour l'insertion, la récupération et la recherche de contacts.
3.  **Permissions Android** : Configuration du manifeste pour autoriser la lecture des contacts et l'accès à Internet.
4.  **Interface Utilisateur** : Création d'un layout avec RecyclerView pour l'affichage fluide des données.
5.  **Communication Réseau** : Utilisation de la bibliothèque Retrofit pour transformer les objets Java en JSON et communiquer avec le serveur.
6.  **Logique Applicative** : Implémentation du ContentResolver pour extraire les données du répertoire et gestion des appels asynchrones vers l'API.
![](https://github.com/user-attachments/assets/509a77ca-23d7-40eb-8c50-4b98559432fe)
---

## Questions de compréhension

**Quel est le rôle de ContentResolver dans Android ?**
Le ContentResolver agit comme un intermédiaire entre l'application et les fournisseurs de données du système (Content Providers). Il permet d'interroger, d'insérer ou de modifier des données partagées par d'autres applications, comme le carnet d'adresses, sans avoir à connaître la structure interne de leur base de données.

**Pourquoi faut-il demander READ_CONTACTS ?**
Le répertoire téléphonique contient des données privées et sensibles. Android impose donc une permission explicite pour protéger la vie privée de l'utilisateur. Depuis Android 6.0, cette permission doit être demandée dynamiquement au moment de l'exécution pour que l'utilisateur puisse l'accepter ou la refuser.

**Quelle différence existe entre RecyclerView et ListView ?**
Le RecyclerView est une évolution plus performante de la ListView. Son rôle principal est de recycler les vues : au lieu de créer un élément graphique pour chaque ligne de la liste, il réutilise les éléments qui sortent de l'écran pour afficher les nouveaux. Cela rend l'application beaucoup plus fluide, surtout avec de grandes quantités de données.

**Quel est le rôle de Retrofit ?**
Retrofit est une bibliothèque qui simplifie les appels HTTP vers un serveur distant. Elle permet de transformer une interface Java en un client REST complet. Elle gère automatiquement la conversion des données (par exemple du JSON vers des objets Java) et facilite la gestion des erreurs réseau.

**Pourquoi utiliser enqueue(...) au lieu d’un appel synchrone ?**
Un appel réseau peut prendre du temps. Si on utilise un appel synchrone sur le thread principal (UI Thread), l'application "gèle" et devient inutilisable jusqu'à la réponse du serveur. La méthode `enqueue()` lance la requête en arrière-plan (asynchrone), permettant à l'interface de rester réactive pendant que les données sont chargées.

**Pourquoi le backend renvoie-t-il du JSON ?**
Le JSON (JavaScript Object Notation) est un format de texte léger, facile à lire par les humains et très rapide à analyser par les machines. C'est le standard universel pour l'échange de données entre un serveur et une application mobile, car il est indépendant du langage de programmation utilisé (PHP d'un côté, Java de l'autre).

**Pourquoi le numéro de téléphone est-il stocké sous forme de chaîne (String) ?**
Un numéro de téléphone n'est pas un nombre mathématique sur lequel on effectue des calculs (additions, multiplications). De plus, les numéros commencent souvent par un zéro (qui disparaîtrait avec un format entier) ou contiennent des caractères spéciaux comme le signe plus (+), des espaces ou des tirets.

**Quel est l’intérêt des requêtes préparées en PHP ?**
Les requêtes préparées permettent de séparer la structure de la commande SQL des données fournies par l'utilisateur. Cela améliore les performances si la requête est répétée plusieurs fois, mais surtout, cela protège la base de données contre les injections SQL, une faille de sécurité majeure.
