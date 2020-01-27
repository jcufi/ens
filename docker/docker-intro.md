<style>
.reveal pre{
        box-shadow: 0px 0px 0px;
}
</style>

### Présentation docker - CATI XXX
---------------------------

---
#### Présentation docker - CATI XXX
---------------------

1. Docker introduction

2. Docker pour l'utilisateur

3. Docker pour le développeur

4. Retours d'expérience


---
#### Docker introduction
---------------------
*Contexte : Qui l'a crée et pourquoi ?*

* Docker est un projet OpenSource sous licence Apache crée en 2013 par Solomon Hykes.
* Le projet est supporté par la communauté et par l'entreprise Docker Inc.
* TODO :Activité sur github ?
* TODO :pourquoi

---
#### Docker introduction
---------------------

*Qu'est-ce que c'est ?*

Docker est une technologie permettant d'exécuter une application dans un environnement isolé, comprenant l'application mais également l'ensemble des dépendances nécessaires a son fonctionnement.

---
#### Docker introduction
---------------------
*Quelques mots de vocabulaire...*

* L'environnement dans lequel s'exécute l'application est appelé un ***conteneur Docker***.

* La matrice servant a définir ce qui est présent dans le conteneur est appelé une ***image Docker***.

* Un catalogue public d'images accessible sur le web permet de les mutualiser, ce catalogue s'appelle le ***DockerHub***.

---
#### Docker introduction
---------------------

*Comment ça marche ?*

Docker s'appuie sur les fonctionnalités d'isolation du noyau Linux (cgroup, namespaces, ...) pour fournir un environnement d'éxecution étanche.

<!--Parmis ces fonctionnalités citons les espaces de nom Linux (isolation du système de fichier, des processus, du  réseau), et les groupes de contrôle (limitation des ressources)-->


&rArr; L'utilisation de Docker requiert des privilèges élevés sur la machine
<!-- .element: class="fragment" -->

---
#### Docker introduction
---------------------

*Comment je l'utilise ?*
* Docker est disponible sur Linux / Windows / Mac
* Docker s'appuie sur une architecture client/serveur, un client en ligne de commande envoie des instructions (via une API REST) au serveur (daemon linux).


&rArr; On l'utilisera donc au travers de lignes de commandes ...
<!-- .element: class="fragment" -->

---
#### Docker : Premier cas d'utilisation
---------------------

*Je souhaite démarrer une base postgres v12 pour effectuer quelques tests.*

1. Recherche d'une image existante sur DockerHub


---
#### Docker : Premier cas d'utilisation
---------------------

2. Démarrage d'un conteneur basé sur l'image postgres:12

Le client interroge le DockerHub, et télécharge l'image

```bash 
$docker run -it postgres:12
Unable to find image 'postgres:12' locally
12: Pulling from library/postgres
8ec398bc0356: Downloading [====>]  11.72MB/27.09MB
65a7b8e7c8f7: Download complete
b7a5676ed96c: Download complete
```

---
#### Docker : Premier cas d'utilisation
---------------------

Une fois l'image téléchargé le conteneur est démarré,
la base est prête a être utilisée

```bash 
PostgreSQL init process complete; ready for start up.
listening on IPv4 address "0.0.0.0", port 5432
database system is ready to accept connections
```

&rArr; Youpi
<!-- .element: class="fragment" -->

---
#### Docker : Premier cas d'utilisation
---------------------

Le conteneur est un environnement isolé de l'hôte donc *par défaut* :
* Pas de communication réseau
* Pas de partage de données

&rArr; Association de port hôte/conteneur
<!-- .element: class="fragment" -->

&rArr; Montage d'un volume partagé
<!-- .element: class="fragment" -->

<!--*Correspondance entre un port de l'hôte et le port du container ?*-->
<!--*Création d'un point de montage entre le conteneur et l'hôte*-->


---
#### Docker introduction
---------------------

L'image est déjà téléchargé

```bash 
$docker volume create pgdata
pgdata
$docker run -it -p 5432:5432 
            -v pgdata:/var/lib/postgresql/data postgres:12

```



---
#### Docker introduction
---------------------

Si je souhaite démarrer une application dont l'image est présente sur le DockerHub
Lorsque je tape la commande :
1. le démon docker va télécharger le fichier image
2. le démon va executer l'ensemble des instructions présente dans l'image, cette étape est appelée le ***build*** de l'image
3. un conteneur va démarrer afin de rendre l'application accessible sur mon poste


#### Docker introduction
---------------------
*Démonstration*

```bash
$ docker run --rm chuanwen/cowsay
 ________________________________________ 
/ In defeat, unbeatable; in victory,     \
| unbearable.                            |
|                                        |
\ -- W. Churchill, on General Montgomery /
 ---------------------------------------- 
        \   ^__^                          
         \  (oo)\_______                  
            (__)\       )\/\              
                ||----w |                 
                ||     ||                 
```

* Du point de vue de l'application, celle ci s'execute dans sa distribution Linux spécifique et avec son propre système de fichiers.
    
---
#### Docker introduction
-------------------------

L'image Docker :

```bash
FROM ubuntu:14.04
MAINTAINER Chuanwen Chen "chuanwen@gmail.com"

RUN apt-get update && apt-get install -y cowsay fortunes \
    && rm -rf /var/lib/apt/lists/*

CMD /usr/games/fortune -a | /usr/games/cowsay
```


---
#### Docker introduction
---------------------



---
#### Docker introduction
---------------------

*Je fais déjà ça avec mes machines virtuelles !*

Dans une machine virtuelle, tout le hardware est émulé ce qui est beaucoup moins performant.



   

