# Projet Fig - Géométrie Computationnelle en Necroml

Projet de M2 SIF - ASM (Analyse Sémantique et Modèles)

Un interpréteur de langage dédié à la géométrie computationnelle, écrit en Necroml (un langage fonctionnel avec monade). Le projet implémente des opérations géométriques sur des points, segments et polygones (avec support des trous).

Une bibliothèque d'opérations géométriques élémentaires a d'abord dû être écrite en OCaml. Ces opérations incluent :
- Égalité de points, segments, polygones
- Test d'inclusion de points dans segments et polygones
- Intersection segment-segment
- Intersection segment-polygone
- Opérations sur polygones (intersection, union, différence)

## 🚀 Lancement rapide

```bash
git clone https://github.com/rombiere/semantics_of_geometrical_figures.git 
cd semantics_of_geometrical_figures
opam install camlgpc
dune build
dune exe semantics_of_geometrical_figures
```

## ✨ Fonctionnalités

### Types géométriques supportés
- **Point** : coordonnées (x, y)
- **Segment** : paire de points
- **Polygon** : polygone avec ring extérieur et trous optionnels
- **Geometry** : collection de figures géométriques

### Opérations implémentées

#### Opérations booléennes
- **Égalité** (`Eq`) : teste l'égalité entre deux géométries
- **Intersection** (`Intersects`) : teste si deux géométries s'intersectent
- **Inclusion** (`Includes`) : teste si une géométrie contient une autre
- **IsEmpty** : teste si une géométrie est vide

#### Opérations géométriques
- **Intersection** (`Intersection`) : calcule l'intersection de deux géométries
- **Union** (`Union`) : calcule l'union de deux géométries
- **Différence** (`Difference`) : calcule la différence A \ B
- **Différence symétrique** (`SymmetricDifference`) : calcule (A \ B) ∪ (B \ A)

### Fonctionnalités avancées
- Support des polygones avec trous
- Gestion des intersections segment-segment, segment-polygone, polygone-polygone
- Opérations ensemblistes sur les géométries complexes
- Sémantique opérationnelle avec environnement de variables

## 🔧 Prérequis

### Logiciels requis
- **OCaml** >= 5.1.1 (testé avec 5.4.0 installé localement)
- **Opam** >= 2.1 (gestionnaire de paquets OCaml, testé avec 2.4.1)
- **Dune** >= 3.20 (système de build, testé avec 3.20.2)

### Dépendances
- **Necroml** : Compilateur pour le langage dédié
- **Alcotest** : Framework de tests unitaires

### Installation des dépendances

```bash
# Initialiser Opam (si première utilisation)
opam init

# Créer un switch OCaml
opam switch create necro

# Installer les dépendances
opam install dune alcotest camlgpc

# Installer Necroml
eval $(opam env)
opam repository add necro https://gitlab.inria.fr/skeletons/opam-repository.git#necro
opam install necrolib

```

## 🚀 Installation et Utilisation

### Compiler le projet

Placez-vous à la racine du projet, puis :

```bash
dune build
```

### Exécuter le programme principal

Le programme principal exécute plusieurs exemples d'opérations géométriques :

```bash
dune exec semantics_of_geometrical_figures
```

**Sortie attendue :**
```
=== EXEMPLES ===

=== Ex1: A ∩ B, A ∪ B, A Δ B, A \ B ===
A = Poly[(0.0,0.0),(4.0,0.0),(4.0,4.0),(0.0,4.0)]
B = Poly[(2.0,2.0),(6.0,2.0),(6.0,6.0),(2.0,6.0)]
A ∩ B = Poly[(4.0,2.0),(4.0,4.0),(2.0,4.0),(2.0,2.0)] 
A ∪ B = Poly[(4.0,0.0),(4.0,2.0),(6.0,2.0),(6.0,6.0),(2.0,6.0),(2.0,4.0),(0.0,4.0),(0.0,0.0)] 
A Δ B = Poly[(4.0,4.0),(4.0,2.0),(6.0,2.0),(6.0,6.0),(2.0,6.0),(2.0,4.0)]; Poly[(4.0,0.0),(4.0,2.0),(2.0,2.0),(2.0,4.0),(0.0,4.0),(0.0,0.0)]
A \ B = Poly[(4.0,0.0),(4.0,2.0),(2.0,2.0),(2.0,4.0),(0.0,4.0),(0.0,0.0)]

=== Ex2: Associativité : A ∪ (B ∪ C) = (A ∪ B) ∪ C ===
Résultat du test d'égalité: True
Résultat attendu: True

=== Ex3: (A ∪ B) ⊇ (A ∩ B) ===
Résultat du test d'inclusion: True
Résultat attendu: True

=== Ex4: Distributivité : A ∩ (B ∪ C) = (A ∩ B) ∪ (A ∩ C) ===
Résultat du test d'égalité: True
Résultat attendu: True

=== Ex5: A ∪ B = A Δ B ===
Résultat du test d'égalité: False
Résultat attendu: False

=== Ex6: Distributivité de la différence sur l'union : A \ (B ∪ C) = (A \ B) ∪ (A \ C) ===
Résultat du test d'égalité: False
Résultat attendu: False

=== FIN ===
```

**Note :** Les A, B et C dans les exemples ne sont pas toujours les mêmes

## 📁 Architecture du projet

```
semantics_of_geometrical_figures/
├── README.md                 # Ce fichier
├── dune-project              # Configuration Dune
├── semantics_of_geometrical_figures.opam           # Fichier de dépendances Opam
│
├── bin/                      
│   ├── dune                  # Configuration de build
│   ├── fig.sk                # Spécification Skell du langage
│   └── main.ml               # Programme principal avec exemples
│
├── lib/                      # Bibliothèques (vide actuellement)
│   ├── dune
│   └── figure_utils.ml       # Utilitaires géométriques (GPC)
│
└── test/                    
    ├── dune
    └── geometry_tests.ml     # Suite de tests des primitives géométriques
```

## 🧪 Tests

Le projet utilise **Alcotest** pour les tests unitaires. Les tests couvrent les implémentations primitives géométriques en OCaml.
### Lancer les tests
```bash
dune test
```

Deux tests échouent en raison des limitations suivantes :

Les polygones partageant plusieurs arêtes présentent des instabilités dans la bibliothèque GPC lors du calcul des intersections ou unions, provoquant des résultats imprévisibles et des échecs d'assertions dans les tests. Ces instabilités numériques sont des limitations inhérentes de la dépendance de la bibliothèque géométrique utilisée.

## 📚 Références

- [Necroml](https://github.com/pedagand/necroml) - Compilateur Necroml
- [GPC](http://www.cs.man.ac.uk/~toby/alan/software/) - General Polygon Clipper
- [Dune](https://dune.readthedocs.io/) - Documentation Dune
- [Alcotest](https://github.com/mirage/alcotest) - Framework de tests

## 👥 Auteur

Projet réalisé par Paul Laurent dans le cadre du cours ASM (Advanced Semantics) du M2 SIF

