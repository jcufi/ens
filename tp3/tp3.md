### Retour en Laponie
---------------------------
---
#### Vue globale
-------------------------
![schema complet](uml4/tp3.svg)

(sans attributs ni opérations)

---
#### Classe Abstraite
---------------------

* Classe "générale" qui occupe un rang élevé dans la hierarchie des classes
    * Ne peut pas être instanciée
    * Peut contenir des méthodes abstraites (sans corps)
    > Si une classe contient au moins une méthode abstraite, alors il faut déclarer cette classe
    abstraite

---
#### Classe abstraite
---------------------
<pre><code>
public abstract class ObjetPostal {
    ...
    abstract public double getTarifBase();
    
    public double tarifAff(){
        double t=this.getTarifBase();
        if (this.getTauxRec().equals(TauxRecom.moyen)) t+=0.5;
        else 
            if (this.getTauxRec().equals(TauxRecom.fort)) t+=1.5;
        return t;
    }
    
    abstract public double tarifRemb();
}
</code></pre>

---
#### Héritage - attributs
------------------
<div style="float:left;width:20%;">
<img src="uml2/ColisExpress.svg" />
<small>(Sans opérations)</small>
</div>

</div>
<div style="float:right;width:80%;">
<pre><code>
public class Colis extends ObjetPostal {
    private String declContenu;
    private double valeurDecl;
    private static double tarifBase=2;
}
</code></pre>

<pre><code>
public class ColisExpress extends Colis {
    private Date dateEnvoi;
    private final int numeroSuivi;
    private boolean emballage;
    private static int numeroCourant=0;
    private static double tarifEmballage=3;
    private static double tarifBase=30;
}
</code></pre>
</div>

---

#### Héritage - Opérations 
------------------
![](uml5/ObjetPostal.svg)

<small>(sans attributs)</small>

---

#### Héritage - Opérations
------------------
<pre><code>
public abstract class ObjetPostal {
    public double tarifAff(){
        double t=this.getTarifBase();
        if (this.getTauxRec().equals(TauxRecom.moyen)) t+=0.5;
        else 
            if (this.getTauxRec().equals(TauxRecom.fort)) t+=1.5;
        return t;
    }
}
</code></pre>
<pre><code>
public class Colis extends ObjetPostal {
    @Override
    public double tarifAff() {
        double t = super.tarifAff();
        if (this.getVolume()>1.0/8.0){ t+= 3; }
        return t;
    }
}
</code></pre>

---
#### Héritage - Redéfinition de méthode
------------------
<div style="float:left;width:20%;">
<img src="uml3/ColisExpress.svg" />
</div>

</div>
<div style="float:right;width:80%;">
<pre><code>
public class Colis extends ObjetPostal {
    @Override
    public double tarifAff() {
        double t = super.tarifAff();
        if (this.getVolume()>1.0/8.0) t+= 3;
        return t;
    }
}
</code></pre>

<pre><code>
public class ColisExpress extends Colis {
    public double tarifAff() {
        double t = this.getTarifBase();
        if (this.emballage){
            t+= ColisExpress.tarifEmballage;
        } 
        return t;
    }
}
</code></pre>
</div>

---

#### Polymorphisme - Transformation de type
------------------

> Une référence sur un objet d’une sous-classe peut toujours être implicitement convertie
en une référence sur un objet de la super-classe.

<pre><code>ObjetPostal o = new Lettre();</code></pre>
<small>ou</small>
<pre><code>Colis c = new ColisExpress();</code></pre>

---
#### Polymorphisme des opérations
------------------
<pre><code>
public static void main(String args[]){
    Colis o3 = new ColisExpress("pole sud", "Paris", "75000",...);
    System.out.println(o3.toString()); 
}
</code></pre>

La méthode toString() appelée est celle de la classe ColisExpress
<small>
* Le code de la méthode qui sera réellement exécuté n’est pas figé
* Un appel de message autorisé à la compilation donnera des résultats différents à l’exécution
* Le langage retrouve selon l’objet et la classe à laquelle il doit son existence le code à exécuter (on parle de liaison dynamique).

</small>