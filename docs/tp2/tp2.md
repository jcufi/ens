<style>
.reveal pre{
        box-shadow: 0px 0px 0px;
}
</style>

#### TD/TP 2 - Classes, attributs, et méthodes en UML et Java
---------------------------


---
#### Rappel de cours - Constructeur
---------------------

* Un constructeur est une opération particulière d’une classe qui permet de créer des instances de cette classe.

* En UML on précise qu'une opération est un constructeur au travers du stéréotype << create >>

<img src="uml/Rectangle_const.svg"  style="width:60%;height:60%;border-style:none;" /> 

<small>(diagramme partiel)</small>

---
#### Rappel de cours - Accesseur
---------------------

* Les accesseurs sont des méthodes qui permettent d’accéder aux attributs, en lecture et en écriture.
<div style="float:left;width:35%;height:100%;">
<img src="uml/Rectangle_accesseur.svg"  style="width:100%;height:100%;border-style:none;" /> 
<p style="text-align:center;"><small >(diagramme partiel)</small></p>
</div>
<div style="float:right;width:65%">
<pre ><code style="overflow-y:hidden;height:100%;">
public class Rectangle {
    private float longueur;
    public float getLongueur() {
		return longueur;
	}
	public void setLongueur(float longueur) {
		this.longueur = longueur;
	}
    ...
}
</code></pre>
</div>

---

#### Diagrammes de classe
------------------

<img src="uml2/Etudiant.svg" style="border-style:none;" />
<img src="uml2/Note.svg" style="border-style:none;" />
<img src="uml2/Module.svg" style="border-style:none;" />
<img src="uml2/Mention.svg" style="border-style:none;" />

<small>(Sans opérations)</small>

</div>

---
#### Diagramme de la classe Etudiant
-------------------------

<img src="uml/Etudiant_sans_accesseurs.svg"  style="width:100%;height:100%;border-style:none;" /> 

<small>(Sans Accesseurs)</small>
---

#### Diagramme de la classe Etudiant
-------------------------

<img src="uml/Etudiant.svg"  style="width:75%;height:75%;border-style:none;" /> 
<small>(Avec opérations et accesseurs)</small>

---

#### Diagramme des classes Module, Note
-------------------------

<img src="uml3/Module.svg"  style="border-style:none;" /> 


<img src="uml3/Note.svg"  style="border-style:none;" /> 

---
#### Question 3a

* Résultat par défaut de toString() sur un objet
```bash
java.lang.Object@6d6f6e28
```
* Résultat de toString() sur un objet Etudiant avec redéfinition
```bash
Nom étudiant :Jean
```

> Par défaut toString() retourne un hashcode, adresse de l’objet en mémoire

---
#### Question 3b

* Méthode toString() de la classe Etudiant

```java
public String toString() {
		return "Nom étudiant :" + this.getNom();
}
```
* Méthode toString() de la classe Module

```java
public String toString() {
    return "Nom module : " + this.getNom();
}
```

* Méthode toString() de la classe Note

```java
public String toString() {
    return "Note : " + getValeur() + " " + module.toString();
}
```
---
#### Question 4

* Méthode calculerAge de la classe Etudiant

```java
/**
* Calcule l'age de l'étudiant en se basant sur la date de naissance
* 
* @return l'age de l'étudiant
*/
public int calculerAge() {
 Long ageEnMillisecondes;
 Long ageEnAnnees;
 ageEnMillisecondes = new GregorianCalendar().getTimeInMillis();
 ageEnMillisecondes = ageEnMillisecondes - dateNaissance.getTime();
 ageEnAnnees = ageEnMillisecondes / (1000L * 60 * 60 * 24 * 365);
 return ageEnAnnees.intValue();
}
```