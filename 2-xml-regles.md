XML – introduction
===

Pour les exercices, on utilise l’éditeur [Atom](https://atom.io/).  
Installer les packages (`Preferences… > Install > Install Packages`) :
* `linter` (avec ses dépendances: `linter-ui-default`, avec ses dépendances: `intentions`, `busy-signal`)
* `linter-autocomplete-jing` (pour autocomplétion)


# eXtensible Markup Language
* [X**ML**](https://fr.wikipedia.org/wiki/Extensible_Markup_Language) : **Markup Language**, XML est un langage à balises.
* **X**ML : XML est **eXtensible** → permet de définir différents “espaces de noms” (***namespace***).
* XML ne propose pas un jeu prédéfini et fermé de balises, mais des règles sur ce
que doit être un document **bien formé** et **valide**.
* Objectifs : faciliter l’échange de contenus.
* Principes :
  * la structure d’un document XML est définie et validable par un **schéma** ;
  * un document XML est transformable en un autre document XML.

# CONFORMITÉ XML

## Premier document XML
```xml
<?xml version="1.0" encoding="UTF-8"?>
<document xmlns="URI/de/mon/espace-de-nom">
  <métadonnées>
    <auteur>Vincent</auteur>
    <date when="2017">2017</date>
    <titre>Du texte brut aux balises</titre>
  </métadonnées>
  <texte>
    <partie>
      <titre>Texte brut</titre>
      <paragraphe>Le texte brut (<locEtrangere xml:lang="en">plain text</locEtrangere>) représente le contenu basique et échangeable et inter-opérable du texte.</paragraphe>
      <paragraphe>...</paragraphe>
    </partie>
    <partie>
      <titre>Langages de balise</titre>
      <paragraphe>Les langages de balises (<locEtrangere xml:lang="en">Markup Languages</locEtrangere>) permettent l'enrichissement d'information textuelle.</paragraphe>
      <paragraphe>...</paragraphe>
    </partie>
  </texte>
</document>
```
## Balise, élément
**Balise**
* balise ouvrante : `<titre>`
* balise fermante : `</titre>`
* NB : une balise peut contenir d’autres balises.

**Élément**
* `<titre>Première partie</titre>`
* = balise ouvrante + contenu + balise fermante.

**Syntaxe**
* Les noms des balises **doivent** commencer par une lettre ou "`_`", les caractères suivants peuvent être des chiffres, des lettres, "`_`", "`.`" ou "`-`".
* **La casse est signifiante**. Les balises peuvent être en majuscules ou en minuscules (ou les deux) :  
les balises `<titre>`, `<Titre>` et `<TITRE>` ne sont pas les mêmes.

**Nœud de type texte** : “Première partie”

## Attribut
`xmlns="URI/de/mon/espace-de-nom"`  
`when="2017-11"`  
`xml:lang="lat"`
* Une paire nom="valeur", intégrée à la balise
* Séparé du nom de la balise par une espace
* Valeur de l’attribut entre *double quotes* : "valeur"

## Document bien formé (règles XML)
### Déclaration XML
Un document XML commence par la **déclaration XML** (`<?xml version="1.0" encoding="UTF-8"?>`) qui précise :
  * la version de la norme XML (`version="1.0"`) ;
  * éventuellement l’encodage utilisé (`encoding="UTF-8"`), **par défaut UTF-8**.

### Élément racine
Le document contient un **UNIQUE élément racine** (ici `document`).  
L’élément racine précise aussi l’**espace de noms** (`namespace`) utilisé (`xmlns="URI/de/mon/espace-de-nom"`).

### Fermeture des balises
**Toute balise ouverte doit être refermée** : (`<texte>` est refermée avec `</texte>`).  
Si une balise est **vide** (si elle ne contient pas de texte), elle peut être simplifiée en une **balise auto-fermante** : en TEI, on écrit `<pb/>` pour `<pb></pb>` ("*page beginning*").

### Imbrication
**Les balises doivent-être imbriquées** : une balise ouverte ne peut pas être fermée tant que toutes les balises incluses dedans n’ont pas été fermées.  
Autrement dit, les balises ne peuvent pas se "chevaucher".

**NON CONFORME (PAS BIEN) :**
```xml
<a>
  <b>
</a>
  </b>
```
**CONFORME (BIEN) :**
```xml
<a>
  <b>
  </b>
</a>
```

## Un arbre
Un document XML représente syntaxiquement un arbre.
> TODO: dessiner l’arbre du document

## <span style="color:orange">Exercice 1. Écrire un premier document XML</span>
> Baliser cette première page du *Misanthrope*
> * Lister les éléments et les attributs utiles pour encoder le début de cette scène.  
> **NB.** Nous faisons le **choix de représenter la structure sémantique** (acte, scène, etc.) plutôt que la structure matérielle de la page (marge, espacement, lignes de séparation, etc.).
> * Enrichir la transcription texte brut ([misanthrope.txt](./docs/misanthrope.txt)) avec les balises définies pour contruire le fichier XML.  
> **NB.** N’oubliez pas la déclaration XML en tête de fichier.  
> **NB.** Pensez à indenter votre fichier.

![Première page du Misanthrope](./img/misanthrope.png)

### Exercice 1. Correction
**Éléments** retenus (en cours) : `piece`, `acte`, `scene`, `titre`, `casting` (la liste des personnages de la scène), `tourDeParole`, `didascalie`, `vers`.

**Attributs** retenus (en cours) : `@aligner` (pour décrire l’alignement de certains vers, éventuellement des tours de parole), `@xml:lang` (préciser la langue de la pièce).

**Premier fichier XML**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<piece xml:lang="fr">
  <titre>LE MISANTHROPE.</titre>
  <acte>
    <titre>ACTE PREMIER</titre>
    <scene>
      <titre>SCÈNE 1.</titre>
      <casting>PHILINTE, ALCESTE</casting>
      <tourDeParole>PHILINTE.</tourDeParole>
      <vers>Qu'est-ce donc? qu'avez-vous ?</vers>
      <tourDeParole>ALCESTE<didascalie>, assis</didascalie>.</tourDeParole>
      <vers aligner="droite">Laissez-moi, je vous prie.</vers>
      <tourDeParole>PHILINTE.</tourDeParole>
      <vers>Mais encor, dites-moi, quelle bizarrerie....</vers>
      <tourDeParole>ALCESTE.</tourDeParole>
      <vers>Laissez-moi là, vous dis-je, et courez vous cacher.</vers>
      <tourDeParole>PHILINTE.</tourDeParole>
      <vers>Mais on entend les gens au moins sans se fâcher.</vers>
      <tourDeParole>ALCESTE.</tourDeParole>
      <vers>Moi, je veux me fâcher, et ne veux point entendre.</vers>
      <tourDeParole>PHILINTE</tourDeParole>
      <vers>Dans vos brusques chagrins je ne puis vous comprendre,</vers>
      <vers>Et quoique amis enfin, je suis tout des premiers....</vers>
      <tourDeParole>ALCESTE<didascalie>, se levant brusquement</didascalie>.</tourDeParole>
      <vers>Moi, votre ami? Rayez cela de vos papiers.</vers>
      <vers>J'ai fait jusques ici profession de l'être,</vers>
      <vers>Mais, après ce qu'en vous je viens de voir paraître,</vers>
    </scene>
  </acte>
</piece>
```

## <span style="color:orange">Exercice 2. Conformité XML</span>
> * Ouvrir ce premier fichier XML ([misanthrope.xml](./docs/misanthrope.xml)) dans Atom (ou Oxygen XML Editor).
> * Faire des erreurs de syntaxe (élément mal refermé, valeur d’attribut hors *double quotes*, etc.).
> * **Lire les message d’erreur** de `Jing` (`Linter`) et…
> * **…comprendre ce qu’est un fichier bien formé.**

# VALIDITÉ XML

XML ne propose pas de balises prédéfinies. La structure d’un document doit être spécifiée :
* quelles balises ? quels attributs ?
* quelles sont les règles d’imbrication de ces balises ?

Langages de schéma
* [DTD (Document Type Definition)](https://fr.wikipedia.org/wiki/Document_Type_Definition)
* [Relax-NG](https://fr.wikipedia.org/wiki/Relax_NG)
* XML Schéma (XSD), Schematron, ODD...

## <span style="color:orange">Exercice 3. Schéma et validité XML</span>
> * Pour chaque élément retenu pour la transcription du *Misanthrope*, définir en une petite phrase les règles d’imbrication avec les autres éléments.
> * Formaliser une DTD.

### Exercice 3. Correction
**Définition du schéma (documentation)**
* `piece` : élément racine ; une `piece` contient d’**abord** ***un*** `titre` **puis** ***des*** `acte`(s).
* `acte` : un `acte` contient d’**abord** ***un*** `titre` **puis** ***des*** `scene`(s).
* `scene` : une `scene` contient d’**abord** ***un*** `titre`, **puis** ***un*** `casting`, **suivis** de ***plusieurs groupes*** composés (d’***un*** `tourDeParole` **puis** ***un ou plusieurs*** `vers`).
* `titre` : du texte.
* `casting` : du texte.
* `tourDeParole` : du texte **mêlé** ***éventuellement avec une*** `didascalie`.
* `didascalie` : du texte.
* `vers` : `@aligner`, du texte.
* `@aligner`: décrire éventuellement l’alignement.

**Définition du schéma (DTD)**
```dtd
<!DOCTYPE piece [
  <!ELEMENT piece (titre, acte+)><!-- Une pièce contient un titre puis des actes. -->
  <!ATTLIST piece xml:lang CDATA #REQUIRED><!-- Une pièce a un attribut langue. -->
  <!ELEMENT acte (titre, scene+)><!-- Un acte contient un titre puis des scènes. -->
  <!ELEMENT scene (titre, casting, (tourDeParole, vers+)+)><!-- Une scène contient d’abord un titre, puis un casting, suivis de plusieurs groupes composés d’un tourDeParole suivi d’un ou plusieurs vers. -->
  <!ELEMENT titre (#PCDATA)><!-- Du texte (Parsed Character Data). -->
  <!ELEMENT casting (#PCDATA)><!-- Du texte. -->
  <!ELEMENT tourDeParole (#PCDATA | didascalie)*><!-- Du texte mêlé éventuellement avec une didascalie. -->
  <!ELEMENT didascalie (#PCDATA)><!-- Du texte. -->
  <!ELEMENT vers (#PCDATA)><!-- Du texte -->
  <!ATTLIST vers aligner (droite|centre) #IMPLIED><!-- Décrire éventuellement l’alignement. -->
]>
```
## <span style="color:orange">Exercice 4. Validité XML</span>
> * Copier/coller cette DTD en tête du fichier `misanthrope.xml` ([misanthrope-DTD.xml](./docs/misanthrope-DTD.xml)).
> * Faire des erreurs de schéma (modifier le nom d’un élément, placer un `titre` là où ce n’est pas prévu, etc.).
> * **Lire les message d’erreur** de `Jing` (`Linter`) et…
> * **…comprendre ce qu’est un fichier valide.**
> * Ajouter une scène, un acte : quels bénéfices tirons-nous de la validation ?

Problème : pouvons-nous échanger nos fichiers (avec des collègues allemands par exemple) ?
