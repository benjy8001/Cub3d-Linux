### Plan :
#### I - Qu'est ce que Cub3d ?
 - Le sujet
 - Le raycasting dans la théorie
#### II - Comment ai-je fait Cub3d ? 11 étapes
 - étape 1  : Parser le fichier .cub
 - étape 2  : Comprendre la minilibx et imprimer des carrés et des triangles
 - étape 3  : Créer la minimap pour apprendre à utiliser la Minilibx
 - étape 4  : Savoir récupérer les keys et les utiliser dans la minimap
 - étape 5  : Le raycasting sans textures dans la pratique
 - étape 6  : La couleur du sol et du plafond
 - étape 7  : Ajouter les textures
 - étape 8  : Les Sprites
 - étape 9  : --save
 - étape 10 : Les derniers petits éléments
 - étape 11 : Les leaks
#### III - Les trucs utiles que j'ai appris
 - Techniques de débogage
 - VIM
 - Git

# I - Qu'est ce que Cub3d ?
### Le sujet
### Le raycasting dans la théorie

# II - Comment ai-je fait Cub3d ? 11 étapes
## étape 1  : Le parsing
### A faire :
- Parser dans un tableau de char à double entrée (il est également possible de parser dans un tableau de int, mais j’ai préféré la solution des chars).
- Checker que la map soit entourée de murs
- A chaque fois faire passer par la fonction qui vérifie que les caractères de la map sont bien des 0,1,2 
- A chaque fois faire passer par la fonction qui vérifie s'il y a bien le joueur dans la map (donc si y a N,S,E ou W) et si le joueur est là remplacer par 0 et retenir dans une variable la position et la direction du joueur
- Faire un tableau de chaînes de caractères
- J'ai ajouté des 1 avant ou après pour que toutes les lignes soit de la taille de la ligne la plus grande
- Pour le malloc de map** je read une première fois pour trouver la taille de la chaîne la plus longue de la map + le nombre de chaînes qu’il y a dans la map
- Malloquer le tableau avec le nombre de char * qu’il y a dedans
- Malloquer ensuite chaine de caractère par chaîne de caractères dans le tableau
- Remplacer tous les espaces par des murs + ajouter des murs au bout pour que la taille de la chaîne soit suffisamment grande

### Rappel du malloc d'un tableau de chaînes de caractères :
  ```
  char **liste;
  char *ptr
  liste = malloc(sizeof(char*) * nbrdechaines)
  liste[i] = malloc(sizeof(char) * ft_strlen(str))
  ```
### Tous les trucs tricky auxquels il faut penser à propos des arguments :
- [x] : Nombre d’arguments invalide : moins de 2 arguments ou plus de 3
- [x] : 3 arguments mais le 3ème n’est pas --save
- [x] : 2 arguments mais un fichier lol.cub.c
- [x] : Fichier .cub n’existe pas
- [x] : Le .cub est un directory

### Tous les trucs tricky auxquels il faut penser pour le parsing de tout sauf la map :
- [x] : Il manque qqe chose (R, NO, SO, S…)
- [x] : Deux fois la même chose (deux R, deux NO..)
- [x] : Résolution avec des int plus grands que int max
- [x] : Résolution avec une virgule ou un autre caractère dedans
- [x] : Résolution avec 3 chiffres, ou un seul, ou un 0
- [x] : F ou C avec un chiffre qui manque, ou un chiffre en trop
- [x] : F ou C avec une virgule en moins ou une virgule en trop 
- [x] : F ou C avec un int supérieur à int max : doit renvoyer une erreur
- [x] : F ou C avec un chiffre supérieur à 255
- [x] : Un identifiant mauvais genre (X au lieu de R, ou E au lieu de EA)

### Tous les trucs tricky auxquels il faut penser pour le parsing de la map :
- [x] : Une ligne vide dans la map : “Sauf pour la map elle-même, les informations de chaque élément peuvent être séparées par un ou plusieurs espace(s)"
- [x] : Un caractère incorrect dans la map, genre un 4
- [x] : Une map ouverte
- [x] : “Les espaces sont une partie valable de la carte, c’est à vous de les gérer correctement” : pour moi les espaces vides sont des murs
- [x] : La map est avant un autre élément 
- [x] : Il n’y a pas de map
- [x] : Pas de joueur ou plusieurs joueurs

## étape 2  : La Minilibx
### Installer la Minilibx :
 - prendre le fichier .xvf sur l’intra
 - faire tar -xvf le fichier
 - copier le libmlx.dylib au niveau des fichiers
 - gcc les .c avec libmlx.dylib
 - faire ./a.out

### 

## étape 4  : Les keys 
### A faire :
- Appuyer sur escape et que ca quitte proprement (pour que ca quitte proprement utiliser exit(0))
- Appuyer sur flèche de gauche : rotation gauche
- Appuyer sur flèche de droite : rotation droite
- Appuyer sur W : avance
- Appuyer sur S : recule
- Appuyer sur A : déplace à gauche
- Appuyer sur D : déplace à droite

### Keycodes :
Linux qwerty :
- define ROTATE_LEFT	65361
- define ROTATE_RIGHT	65363
- define FORWARD_W_Z	119
- define BACK_S_S		115
- define RIGHT_D_D		100
- define LEFT_A_Q		97
Linux azerty :
- define ROTATE_LEFT	65361
- define ROTATE_RIGHT	65363
- define FORWARD_W_Z	122
- define BACK_S_S		115
- define RIGHT_D_D		100
- define LEFT_A_Q		113
Mac qwerty :
define ROTATE_LEFT		123
define ROTATE_RIGHT		124
define FORWARD_W_Z		13
define BACK_S_S			1
define RIGHT_D_D			2
define LEFT_A_Q			0


# III - Les trucs utiles que j'ai appris
