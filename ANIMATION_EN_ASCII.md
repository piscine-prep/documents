# Animation de Cercle en Terminal

## Introduction

Ce programme crée une animation visuelle dans le terminal qui affiche un cercle qui grandit progressivement. Lorsqu'il atteint sa taille maximale, il recommence à zéro et alterne entre deux modes d'affichage : un cercle plein et un cercle vide (contour seulement). Cette animation se déroule en boucle infinie.

```
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||||||• • • • • • • • • • • ||||||||||||||||||||
||||||||||||||||• • • • • • • • • • • • • • • ||||||||||||||||
||||||||||||||• • • • • • • • • • • • • • • • • ||||||||||||||
||||||||||• • • • • • • • • • • • • • • • • • • • • ||||||||||
||||||||• • • • • • • • • • • • • • • • • • • • • • • ||||||||
||||||||• • • • • • • • • • • • • • • • • • • • • • • ||||||||
||||||• • • • • • • • • • • • • • • • • • • • • • • • • ||||||
||||• • • • • • • • • • • • • • • • • • • • • • • • • • • ||||
||||• • • • • • • • • • • • • • • • • • • • • • • • • • • ||||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||• • • • • • • • • • • • • • • • • • • • • • • • • • • • • ||
||||• • • • • • • • • • • • • • • • • • • • • • • • • • • ||||
||||• • • • • • • • • • • • • • • • • • • • • • • • • • • ||||
||||||• • • • • • • • • • • • • • • • • • • • • • • • • ||||||
||||||||• • • • • • • • • • • • • • • • • • • • • • • ||||||||
||||||||• • • • • • • • • • • • • • • • • • • • • • • ||||||||
||||||||||• • • • • • • • • • • • • • • • • • • • • ||||||||||
||||||||||||||• • • • • • • • • • • • • • • • • ||||||||||||||
||||||||||||||||• • • • • • • • • • • • • • • ||||||||||||||||
||||||||||||||||||||• • • • • • • • • • • ||||||||||||||||||||
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
```

## Prérequis

Pour comprendre et utiliser ce code, vous devez avoir des connaissances de base en programmation C :

- Variables et types de données
- Conditions (if/else)
- Boucles (while, for)
- Fonctions simples

## Compilation et exécution

Pour compiler le programme, utilisez un compilateur C comme gcc :

```
gcc animation_cercle.c -o animation_cercle -lm
```

Le paramètre `-lm` est nécessaire pour lier la bibliothèque mathématique (pour la fonction `sqrt`).

Pour l'exécuter :

```
./animation_cercle
```

Pour arrêter l'animation, appuyez sur Ctrl+C.

## Explication du code

### Les bibliothèques utilisées

```c
#include <stdio.h>  // Pour les fonctions d'entrée/sortie comme printf
#include <unistd.h> // Pour la fonction usleep (pause en microsecondes)
#include <time.h>   // Pour les fonctions liées au temps
#include <math.h>   // Pour la fonction sqrt (racine carrée)
```

### Fonction sleep_ms

```c
void sleep_ms(int milliseconds)
{
    usleep(milliseconds * 1000); // usleep prend des microsecondes
}
```

Cette fonction permet de faire une pause en millisecondes. Comme la fonction `usleep` prend des microsecondes en paramètre, nous multiplions les millisecondes par 1000.

### Configuration initiale

```c
// ---- Configuration de la grille d'affichage ----
int grid_width = 30;  // Largeur de la grille en caractères
int grid_height = 30; // Hauteur de la grille en caractères

// ---- Configuration du cercle ----
int circle_center_x = grid_width / 2;  // Position X du centre du cercle
int circle_center_y = grid_height / 2; // Position Y du centre du cercle
int circle_radius = 1;                 // Rayon initial du cercle

// ---- Variables pour contrôler l'animation ----
int radius_change = 1;    // Direction de changement du rayon: 1=grandir
int animation_delay = 50; // Délai entre chaque image (en millisecondes)
int circle_fill_mode = 1; // Mode de remplissage: 1=plein, 0=contour
```

### La boucle principale de l'animation

```c
while (1) // Boucle infinie (1 est toujours vrai)
{
    // Code de l'animation...
}
```

Cette boucle s'exécute indéfiniment, créant une animation continue.

### Effacer l'écran

```c
printf("\033[H\033[J");
```

Cette ligne utilise des séquences d'échappement ANSI pour:

- `\033[H` : déplacer le curseur en haut à gauche de l'écran
- `\033[J` : effacer tout ce qui suit le curseur

Ces commandes permettent de "rafraîchir" l'écran à chaque itération.

### Dessiner le cercle

```c
// Parcourir chaque ligne de la grille
for (int y = 0; y <= grid_height; y++)
{
    // Parcourir chaque colonne de la grille
    for (int x = 0; x <= grid_width; x++)
    {
        // Calculer la distance entre le point actuel et le centre du cercle
        int distance_x = x - circle_center_x;
        int distance_y = y - circle_center_y;
        double distance = sqrt(distance_x * distance_x + distance_y * distance_y);

        // Décider quoi afficher selon le mode et la position
        if (circle_fill_mode == 0) // Mode contour
        {
            if (distance < circle_radius)
            {
                printf("• "); // Intérieur vide
            }
            else
            {
                printf("||"); // Extérieur rempli
            }
        }
        else // Mode plein
        {
            if (distance < circle_radius)
            {
                printf("||"); // Intérieur rempli
            }
            else
            {
                printf("• "); // Extérieur vide
            }
        }
    }
    printf("\n"); // Nouvelle ligne après chaque rangée
}
```

#### Comment fonctionne le calcul de la distance

La distance entre un point (x,y) et le centre du cercle est calculée grâce au théorème de Pythagore :

- distance = √((x - centre_x)² + (y - centre_y)²)

Si cette distance est inférieure au rayon du cercle, le point se trouve à l'intérieur du cercle.

### Mise à jour pour la prochaine image

```c
// Mettre à jour le rayon pour la prochaine image
circle_radius += radius_change;     // Augmenter le rayon
circle_radius = circle_radius % 25; // Limiter le rayon à 25

// Si le rayon atteint 0, inverser le mode de remplissage
if (circle_radius == 0)
{
    circle_fill_mode = !circle_fill_mode; // Basculer entre 0 et 1
}

// Pause avant la prochaine image
sleep_ms(animation_delay);
```

Après avoir dessiné l'image actuelle:

1. Le rayon est augmenté de 1 (valeur de `radius_change`)
2. L'opération modulo (`%`) assure que le rayon reste entre 0 et 24
3. Si le rayon atteint 0, le mode de remplissage change (de plein à vide ou vice versa)
4. Une pause est effectuée pour ralentir l'animation et la rendre visible

## Concepts mathématiques utilisés

### Le théorème de Pythagore

Pour déterminer si un point se trouve à l'intérieur du cercle, nous calculons sa distance par rapport au centre en utilisant le théorème de Pythagore. Dans un plan cartésien:

Distance = √((x₂ - x₁)² + (y₂ - y₁)²)

Où:

- (x₁, y₁) sont les coordonnées du centre du cercle
- (x₂, y₂) sont les coordonnées du point que nous examinons

### L'opérateur modulo (%)

L'opération modulo (`%`) retourne le reste de la division entière. Dans notre code:

```c
circle_radius = circle_radius % 25;
```

Cela signifie que `circle_radius` prendra des valeurs de 0 à 24, puis reviendra à 0.

## Programme complet

```c
/*
 * Animation de Cercle en Terminal
 *
 * Ce programme crée une animation dans le terminal qui affiche un cercle
 * qui grandit progressivement jusqu'à une taille maximale, puis recommence
 * à zéro. L'animation alterne entre deux modes:
 * - Un cercle plein (rempli de caractères "||")
 * - Un cercle vide (contour seulement)
 *
 * L'animation se poursuit indéfiniment dans une boucle infinie.
 * Le cercle est dessiné dans une grille de caractères en calculant la distance
 * de chaque point au centre du cercle à l'aide du théorème de Pythagore.
 *
 * Ce programme utilise des séquences d'échappement ANSI pour effacer l'écran
 * entre chaque étape de l'animation, créant ainsi un effet visuel fluide.
 */

#include <stdio.h>  // Bibliothèque pour les fonctions d'entrée/sortie standard
#include <unistd.h> // Bibliothèque pour usleep (micro-sleep)
#include <time.h>   // Bibliothèque pour les fonctions liées au temps
#include <math.h>   // Bibliothèque pour les fonctions mathématiques comme sqrt()

// Fonction pour attendre un nombre de millisecondes
void sleep_ms(int milliseconds)
{
    usleep(milliseconds * 1000); // usleep prend des microsecondes
}

int main()
{
    // ---- Configuration de la grille d'affichage ----
    int grid_width = 30;  // Largeur de la grille en caractères
    int grid_height = 30; // Hauteur de la grille en caractères

    // ---- Configuration du cercle ----
    int circle_center_x = grid_width / 2;  // Position X du centre du cercle (milieu de la grille)
    int circle_center_y = grid_height / 2; // Position Y du centre du cercle (milieu de la grille)
    int circle_radius = 1;                 // Rayon initial du cercle (en caractères)

    // ---- Variables pour contrôler l'animation ----
    int radius_change = 1;    // Direction de changement du rayon: 1=grandir, -1=rétrécir
    int animation_delay = 50; // Délai entre chaque image (en millisecondes)
    int circle_fill_mode = 1; // Mode de remplissage: 1=plein, 0=contour seulement

    // Boucle infinie pour l'animation
    while (1)
    {
        // Effacer l'écran en déplaçant le curseur au début (séquence d'échappement ANSI)
        // \033[H : déplace le curseur en haut à gauche
        // \033[J : efface tout depuis la position du curseur jusqu'à la fin de l'écran
        printf("\033[H\033[J");

        // Parcourir chaque ligne de la grille
        for (int y = 0; y <= grid_height; y++)
        {
            // Parcourir chaque colonne de la grille
            for (int x = 0; x <= grid_width; x++)
            {
                // Calculer la distance entre le point actuel (x,y) et le centre du cercle
                // en utilisant le théorème de Pythagore: distance = sqrt((x2-x1)² + (y2-y1)²)
                int distance_x = x - circle_center_x; // Différence en X
                int distance_y = y - circle_center_y; // Différence en Y

                // Utiliser sqrt pour calculer la distance exacte (racine carrée de la somme des carrés)
                double distance = sqrt(distance_x * distance_x + distance_y * distance_y);

                // Mode contour seulement (cercle vide)
                if (circle_fill_mode == 0)
                {
                    if (distance < circle_radius)
                    {
                        printf("• "); // Si à l'intérieur du cercle, afficher un espace
                    }
                    else
                    {
                        printf("||"); // Si à l'extérieur ou sur le cercle, afficher "||"
                    }
                }
                // Mode plein (cercle rempli)
                else
                {
                    if (distance < circle_radius)
                    {
                        printf("||"); // Si à l'intérieur du cercle, afficher "||"
                    }
                    else
                    {
                        printf("• "); // Si à l'extérieur, afficher un espace
                    }
                }
            }

            printf("\n"); // Passer à la ligne suivante après avoir complété une ligne entière
        }

        // ---- Mettre à jour le rayon pour la prochaine image ----
        circle_radius += radius_change;     // Augmenter le rayon (animation d'agrandissement)
        circle_radius = circle_radius % 25; // Limiter le rayon à 25 (retour à 0 après 25)

        // Si le rayon atteint 0, inverser le mode de remplissage (plein <-> contour)
        if (circle_radius == 0)
        {
            circle_fill_mode = !circle_fill_mode; // Basculer entre 0 et 1 (opérateur NOT logique)
        }

        // Pause avant la prochaine image de l'animation
        sleep_ms(animation_delay);
    }

    // Cette ligne ne sera jamais atteinte en raison de la boucle infinie
    return 0;
}
```
