<style>
.reveal pre{
        box-shadow: 0px 0px 0px;
}

</style>

### Présentation docker 
#### CATI DIISCICO 
Julien Cufi - 04/02/2020
<!-- .slide: class="center" -->
---
#### Présentation docker - CATI DIISCICO 
---------------------

1. Docker introduction

2. Docker pour l'utilisateur

3. Docker pour le développeur

4. Retours d'expérience


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

*Je fais déjà ça avec mes machines virtuelles !*

Dans une machine virtuelle, on simule une machine (ie. toute la partie hardware), et le système d'exploitation ce qui est beaucoup plus lourd que de démarrer un conteneur.

![](virtualization-vs-containers.png)

---
#### Docker introduction
---------------------
*Qui l'a crée et pourquoi ?*

* Docker est un projet OpenSource sous licence Apache 2.0 crée en 2013 par Solomon Hykes.
Le projet est supporté par la communauté et par l'entreprise Docker Inc.

* Crée a l'origine pour la société dotCloud (PaaS)

---
#### Docker introduction
---------------------

![](./engine-components-flow.png)

<small>Docker s'appuie sur une architecture client/serveur, un client en ligne de commande envoie des instructions (via une API REST) au serveur (daemon docker).</small>

---
#### Docker introduction
---------------------

*Comment ça marche ?*

A l'origine Docker s'appuie sur LXC (LinuX container) et les fonctionnalités d'isolation du noyau Linux (cgroup, namespaces, ...) pour fournir un environnement d'exécution étanche.

&rArr; Problème portabilité
<!-- .element: class="fragment" -->

---
#### Docker introduction
---------------------

* Remplacement de LXC par libcontainer
* Modularisation de la partie serveur
    * création d'outils spécifiques (creation container, gestion du cycle de vie...)
    * implémentation de référence des spécifications émise par Open Container Initiative...

---
#### Docker introduction
---------------------

Open Container Initiative est un projet de la Fondation Linux pour la normalisation des conteneurs
(environnement d'exécution d'un conteneur, images et référentiel d'images).

<img src="./open_container_project.png" height="80%" width="80%">

<!--Parmis ces fonctionnalités citons les espaces de nom Linux (isolation du système de fichier, des processus, du  réseau), et les groupes de contrôle (limitation des ressources)
UFS-->
<!--&rArr; L'utilisation de Docker requiert des privilèges élevés sur la machine-->

---
#### Docker introduction
---------------------

*Comment je l'utilise ?*

Docker est disponible sur Linux / Windows / Mac (VM)
Deux versions EE et CE (&ne; niveaux de support)



&rArr; On l'utilisera donc au travers de lignes de commandes ...
<!-- .element: class="fragment" -->


---

*passons à la pratique...* 
<!-- .slide: class="center" -->

---
#### Docker : Premier cas d'utilisation
---------------------

*Je souhaite démarrer une base postgres v12 pour effectuer quelques tests.*

Recherche d'une image existante sur DockerHub
https://hub.docker.com/
<img src="./dockerhub.png" height="80%" width="80%">


---
#### Docker : Premier cas d'utilisation
---------------------

Démarrage d'un conteneur basé sur l'image postgres:12

```bash 
$docker run -it postgres:12
Unable to find image 'postgres:12' locally
12: Pulling from library/postgres
8ec398bc0356: Downloading [====>]  11.72MB/27.09MB
65a7b8e7c8f7: Download complete
b7a5676ed96c: Download complete
```
Le client demande le démarrage d'un conteneur, le serveur ne connaissant pas l'image il interroge le DockerHub et la télécharge.

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

&rArr; Youpi ?
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

---
#### Docker introduction
---------------------

*On recommence*

```bash 
$docker volume create pgdata
pgdata
$docker run -it -p 5432:5432 
            -v pgdata:/var/lib/postgresql/data postgres:12

```
Remarque : l'image est déjà téléchargée


---
#### Docker introduction
---------------------

Si je souhaite démarrer une application dont l'image est présente sur le DockerHub
Lorsque je tape la commande :
1. le démon docker va télécharger le fichier image
2. le démon va executer l'ensemble des instructions présente dans l'image, cette étape est appelée le ***build*** de l'image
3. un conteneur va démarrer afin de rendre l'application accessible sur mon poste

<!--Du point de vue de l'application, celle ci s'execute dans sa distribution Linux spécifique et avec son propre système de fichiers.-->

---
#### Docker introduction
---------------------



---
#### Docker introduction
---------------------




---
#### Liens
---------------------
<small>
Lien vers projet OpenSource https://github.com/moby

</small>