# Séparation de sources, projet MVA
Avec un dataset contenant des fichiers audios bruts, la voix isolée et le bruit isolé, on va entraîner plusieurs modèles qui vont essayer de séparer les sources. 
## Première méthode: Deep U-NET sur spectrogramme
La première méthode employée est issue de l'article : "Singing voice separation with Deepu U-NET convolutional network" de Jansson et al. Cette méthode fait l'apprentissage sur les spectrogrammes. Dans l'article, le but est de séparer l'instrumentale et la voix des chansons. On se dit que ça pourrait aussi marcher pour séparer le bruit de la voix. Le but est d'entraîner un modèle qui produit un masque (une matrice) et lorsqu'on multiplie ce masque avec l'input, on est sensé obtenir le spectrogramme de la voix isolée. Naturellement, la loss function associée à une telle idée peut être :
$$
L(X,Y,\theta) = \lVert f(X,\theta)-Y\rVert _1.
$$
$X$ est le spectrogramme de l'input, $Y$ est le spectrogramme de la voix isolée et $\theta$ correspond aux variables du réseau.
On se concentre sur la production d'un bon masque pour isoler la voix, se faisant, on pourra isoler le bruit aussi (en soustrayant $f(X,\theta)$ au spectrogramme initiale).