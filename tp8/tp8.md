### TP8 - Interfaces
----------------------

---
#### Rappel interface

> La notion d’interface permet de  définir un contrat pour un ensemble de classes.

> Par contrat on entend un ensemble d’opérations, incluant des opérations d’accès à des données, 
que l’on s’attend à avoir dans toutes les classes respectant ce contrat.

---
#### Rappel interface
Une interface regroupe :
* des méthodes d'instance 
    <pre><code>public void mamethode();</pre></code>
* des méthodes d'instances abstraites
* des méthodes d'instances publiques par défaut
    <pre><code>public default</pre></code>
* des méthodes statiques
    <pre><code>public static void mamethode(){...}</pre></code>
* des attributs de classe constants public 

---
#### Rappel interface
On ne peut pas mettre :
* de constructeurs
* d'attributs d'instances
* de code dans les méthodes
<small>(en dehors des methodes par défaut et des méthodes statiques)</small>

---
#### Le mot clé "defaut"
* Introduit en Java 8
* Permet d'implementer des méthodes dans l'interface
* Evite de rompre le "contrat" entre l'interface et les classes
<pre  width="100%" height="100%"><code>
package tp7;
import tp6.Personne;
public interface IFileAttente {
	...
    public default String getReglementation(){
		return "sans priorités";
	}
}
</code></pre>
---

#### Modélisation UML

<img src="uml/IFileAttente.svg" style="border:none" width="80%" height="80%" />
<small> Exemple d'interface de la classe FileAttente </small>

---
#### Exemple d'interface

<pre  width="100%" height="100%"><code>
package tp7;
import tp6.Personne;
public interface IFileAttente {
	public void entre(Personne p);
	public Personne sort();
	public int taille();
	public boolean estVide();
	public void vider();
}
</code></pre>

<pre  width="100%" height="100%"><code>
public class FileAttente implements IFileAttente{
...
}
</code></pre>

---
#### Modélisation UML

<img src="uml/tp7.svg" style="border:none" width="80%" height="80%" />

---
#### Exemple d'utilisation d'interface
<pre><code>
public static &lt;E&gt; extends Comparable&lt;E&gt;&gt; E max(List&lt;E&gt; c) {
    if (c.isEmpty()){ return null;}
    E max = c.get(0);
    for (E e : c){ if (e.compareTo(max) > 0){ max = e; }}
    return max;
}
</code></pre>

* La méthode max ne manipule pas de classes directement

> Si on veut l'utiliser avec la classe Etudiant il suffit que la classe Etudiant 
implémente l'interface Comparable

---
#### Interface Comparable
<pre><code>public class Etudiant implements Comparable&lt;Etudiant&gt;{ 
    ...
    @Override
    public int compareTo(Etudiant o) {
        return this.getNom().compareTo(o.getNom());
    }
 }</code></pre>

* L'interface Comparable garantie que les étudiants sont comparables entre eux
et permet donc le tri, la recherche d'un max etc...

<pre><code>// Tri d'une liste d'étudiant par ordre lexicographique
Collections.sort(listeEtudiant);
// Recherche du max
Collections.max(listeEtudiant);
</code></pre>

---
#### Interface Comparator

* Permet d'implementer d'autres façons de comparer deux éléments
* Exemple : Comparer des personnes en fonction de leur age
<pre><code>// Tri d'une liste d'étudiant en fonction de leur age
Collections.sort(listeEtudiant, new ComparateurAge());
</code></pre>
