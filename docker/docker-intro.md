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

*Qu'est ce que c'est ?*

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
*Quelques mots de vocabulaire...*

* Une image Docker est un fichier texte utilisant une syntaxe propre a Docker, il contient un ensemble d'instructions, permettant d'automatiser l'installation de l'application.

* Un catalogue public d'images, hébergé par Docker Inc., est accessible sur le web permet de les mutualiser, ce catalogue s'appelle le DockerHub.

---
#### Docker introduction
---------------------

*Comment ça marche ?*

Docker s'appuie sur les fonctionnalités d'isolation du noyau Linux (lxc, namespace, cgroup) pour fournir un environnement d'éxecution étanche.

<!-- Parmis ces fonctionnalités citons les namespaces Linux (isolation du système de fichier, des processus, du  réseau), et les control group (limitation des resources) -->

---
#### Docker introduction
---------------------
*Qui l'a fait ?*

Docker est un projet OpenSource crée par Salomon Hikes et supporté par l'entreprise Docker Inc


---
#### Docker introduction
---------------------
Démo
``` docker run -it postgres:latest
```

---
#### Docker introduction
---------------------

*Comment je l'utilise ?*

Docker s'appuie sur un système de client/serveur.
Le client en ligne de commande envoie des instructions au serveur (démon linux).



---
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



   

