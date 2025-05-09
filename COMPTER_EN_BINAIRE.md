# Comment compter en binaire

## Introduction

Le système binaire est la base du fonctionnement des ordinateurs. Contrairement à notre système décimal qui utilise 10 chiffres (0-9), le binaire n'utilise que deux chiffres : 0 et 1. Ce document vous explique simplement comment comprendre et utiliser le système binaire.

## Comprendre la valeur des positions

En décimal, chaque position représente une puissance de 10 :

```
      1000  100   10    1
       10³   10²   10¹   10⁰
        |     |     |     |
        V     V     V     V
        1     3     5     2  = 1352 en décimal
```

En binaire, chaque position représente une puissance de 2 :

```
        8     4     2     1
        2³    2²    2¹    2⁰
        |     |     |     |
        V     V     V     V
        1     0     1     1  = 11 en décimal
```

## Tableau de conversion (0-15)

Voici les 16 premiers nombres (0-15) représentés en binaire sur 4 bits :

```
Décimal    Binaire    Calcul
-------    -------    -----------
   0        0000      0+0+0+0 = 0
   1        0001      0+0+0+1 = 1
   2        0010      0+0+2+0 = 2
   3        0011      0+0+2+1 = 3
   4        0100      0+4+0+0 = 4
   5        0101      0+4+0+1 = 5
   6        0110      0+4+2+0 = 6
   7        0111      0+4+2+1 = 7
   8        1000      8+0+0+0 = 8
   9        1001      8+0+0+1 = 9
  10        1010      8+0+2+0 = 10
  11        1011      8+0+2+1 = 11
  12        1100      8+4+0+0 = 12
  13        1101      8+4+0+1 = 13
  14        1110      8+4+2+0 = 14
  15        1111      8+4+2+1 = 15
```

## Visualisation avec des interrupteurs

Une façon simple de visualiser le binaire est d'imaginer des interrupteurs qui peuvent être ALLUMÉS (1) ou ÉTEINTS (0) :

```
     8     4     2     1
     |     |     |     |
     v     v     v     v
    [0]   [0]   [0]   [0]    = 0

    [0]   [0]   [0]   [1]    = 1

    [0]   [0]   [1]   [0]    = 2

    [0]   [0]   [1]   [1]    = 3

    [0]   [1]   [0]   [0]    = 4
```

## Comment compter en binaire

Voici une illustration de l'incrémentation (+1) en binaire de 0 à 15 :

```
0000  (0)
   ↓  (changement du bit le moins significatif)
0001  (1)
   ↓
0010  (2)  <- Le bit "1" se remet à 0 et le bit "2" devient 1
   ↓
0011  (3)
   ↓
0100  (4)  <- Tous les bits précédents se remettent à 0, le bit "4" devient 1
   ↓
0101  (5)
   ↓
0110  (6)
   ↓
0111  (7)
   ↓
1000  (8)  <- Tous les bits précédents se remettent à 0, le bit "8" devient 1
   ↓
1001  (9)
   ↓
1010  (10)
   ↓
1011  (11)
   ↓
1100  (12)
   ↓
1101  (13)
   ↓
1110  (14)
   ↓
1111  (15)
   ↓
(10000) <- Nécessiterait un 5ème bit pour représenter 16 !
```

## Règle simple pour incrémenter

Pour ajouter 1 à un nombre binaire :

1. Si le bit le plus à droite est 0, changez-le en 1
2. Si le bit le plus à droite est 1, changez-le en 0 et passez au bit suivant à gauche
3. Répétez jusqu'à ce que vous changiez un 0 en 1

```
Exemple: 0101 (5) + 1 = ?

0101  <- Le bit le plus à droite est 1, on le change en 0
010↓     et on se reporte au bit suivant
0110  <- Le résultat est 0110 (6)
```

## Relation avec les systèmes informatiques

En informatique :

- 8 bits = 1 octet (peut représenter les nombres de 0 à 255)
- Les caractères sont représentés par des nombres binaires (ex: le caractère 'A' est 01000001 en ASCII)
- Les couleurs sont codées en combinant des valeurs binaires (ex: rouge, vert, bleu)
- Toutes les opérations informatiques se font ultimement en binaire

---

_En comprenant le binaire, vous comprenez le langage fondamental de tous les ordinateurs !_
