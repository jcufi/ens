### TP6 - Bibliothèque
----------------------


---
#### Zoom sur la classe d'association

<img src="uml/diag-classe-assoc.svg" style="border:none" width="100%" height="100%" />

*Une même personne peut être contributrice dans plusieurs ouvrages, avec des roles différents*
---
#### Equivalence
<img src="uml/diag-classe-assoc.svg" style="border:none" width="75%" height="75%" />

<img src="uml/alternative4.svg" style="border:none" width="75%" height="75%" />


---
#### Diagramme d'objets

<img src="uml/diag-objets.svg" style="border:none" width="100%" height="100%" />
<small>
*Daniel Pennac est auteur de "La fée Carabine" et rédacteur de la préface de "Une langue venue d'ailleurs" de Akira Mizubayashi.*</small>

---
#### Exemple de modélisation v1

<img src="uml/diag-full.svg" style="border:none" width="100%" height="100%"  />

---
#### Exemple de modélisation v2
<img src="uml/diag-assoc-qual.svg" style="border:none" width="100%" height="100%"  />

<small>Avec association qualifiée</small>

---
#### Indexation des exemplaires par ISBN

    public class Notice {
        ...
        Hashmap< String, List<Exemplaire>> exemplaires;
        public Notice(){
            exemplaires = new Hashmap< String, List<Exemplaire>>();
        }
    }


