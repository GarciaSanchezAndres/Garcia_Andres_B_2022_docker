# Documentation Projet Docker

L'objectif de ce projet est de créer un site capable d'enregistrer du texte et des images dans un compte personnel, tout ceci grâce à une base de données *Mongo*. Le code javascript, html et css nous étant fourni, notre travail est de créer les conteneurs Docker qui permettent de monter le site en local.
Pour cela l'infrastructure du projet a été divisé en 2 grans répertoires: le frontend et le backend.

**Frontend**: C'est la partie utilisateur du site, on peut cliquer sur des boutons, sur des liens, faire défiler la page de haut en bas, remplir des formulaires, etc. En effet, c'est la partie visuelle du site.

**Backend**: C'est le moteur du site, tout ce qui est derrière et que l'utilisateur ne voit jamais, mais c'est aussice qui lui permet de réaliser toutes les actions sur le frontend. C'est la base de données, le code, etc

Voici a quoi ressemble l'infrastructure de ce projet:

![Whiteboard](https://user-images.githubusercontent.com/82510284/154841435-11010883-39e4-41e2-ba98-8a88e551868f.png)

En effet on va avoir 2 **Dockerfiles**, un pour le frontend et un autre pour le backend. dans ces dockerfiles on va préciser les paramètres d'utilisation du code.

# Dockerfile Frontend
Voici les paramètres qu'on défini dans ce dockerfile:

- L'image qu'on veut télécharger et sa version. Dans ce cas on a utilisé la version 13.12.0-alpine.
- L'utilisation du packet json dans lequel sont définis les paramètres de l'installation de React, un framework frontend très utilisé dans le développement web.
- L'installation de npm, un gestionnaire de paquets Node.
- L'ouverture du port 3000 pour le la partie frontend.

Le code de ce Dockerfile est commenté. 
Voici les commandes utilisées:
-On construit l'image: *docker image build -t app:1.0 .*
-On construit le conteneur: *docker container run -p 3000:3000 app:1.0*

# Dockerfile Backend
Voici les paramètres qu'on défini dans ce Dockerfile backend.
Ce dockerfile est pratiquement pareil à celui du frotend à exception de 2 paramètres

- L'utilisation du paquet json dans lequels sont définis les paramètres de Index.js, le point d'entrée de notre application.
- On ouvre le port 8080 pour la partie backend.

Le code de ce Dockerfile est aussi commenté
Voici la commande a effectué pour créer le conteneur:
-On construit l'image: *docker image build -t app:2.0 .*
-On construit le conteneur: *docker container run -p 8080 app:2.0*

Cependant on ne pourra pas tester que notre partie Backend fontctionne jusqu'à ce qu'on installe notre base de données.

# Docker Compose

Une fois que nos 2 dockerfiles sont scriptés notre site devrait pouvoir être fonctionnel, cependant quand on essaye de créer un compte et s'authentifier une erreur nous est renvoyée. 
En effet, c'est parce qu'on n'a toujours pas de base de données qui puisse stocker nos comptes. Pour cela on va créer un **docker compose**, cet outil va lancer nos conteneurs et leurs éventuels liens à partir d’un fichier de configuration écrit en *.yaml*; C'est l'équivalent d'un apt-get mais dans le but  de packager les conteneurs docker.
Notre compose va contenir un conteneur frontend, un conteneur backend et un base de données Mongo.

Le code du compose est commenté mais on va traiter les aspects les plus importants:

- On build nos 3 images: app1 (frontend), app2 (backend) et mongo
- On ouvre les ports 3000, 8080 et 27017 pour les 3 conteneurs
- On créer nos networks frontend et backend
- On construit un volume pour stocker la data dans la base de données

Une fois que le compose est construit on peut le lancer avec les commandes:
- *Docker compose build*, construit le compose.
- *Docker compose up*, éxecute le compose et met le site en marche.
- Si on veut arreter le compose on peut utiliser, *docker compose down* 

A présent le site est complétement fonctionnel. On peut s'authentifier avec un compte mail réel ou non réel et enregistrer des messages contenant du texte et des images.
Voici une démonstration:

1)On accède au site via localhost:3000

![Capture 1](https://user-images.githubusercontent.com/82510284/154842319-50304679-ec10-4795-bf65-8b6623d7989f.PNG)

2)On clique sur signup et on créer un compte

![Capture 2](https://user-images.githubusercontent.com/82510284/154842400-7d844dc0-2471-48b7-a037-b50808e02c3c.PNG)

3)On se login avec notre nouveau compte

![Capture 3](https://user-images.githubusercontent.com/82510284/154842438-416d47b6-a07a-4363-9291-c8b97adc531b.PNG)

4)En cliquant sur new post on peut créer un message, J'ai créer le message "Image de test pour le projet"

![Capture 4](https://user-images.githubusercontent.com/82510284/154842503-8c1c760a-b137-4644-a2b4-67524a418097.PNG)

5)Voici le message enregistré

![Capture 5](https://user-images.githubusercontent.com/82510284/154842538-73047236-901f-425f-b3f7-e62c79f10569.PNG)






