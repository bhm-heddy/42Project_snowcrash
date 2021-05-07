# LEVEL 14

**LOGIN: level14**

**PASSWORD: 2A31L79asukciNyi8uppkEuSx**

 ----


Bon... une heure de recherches infructueuses.. aucun indice.. rien.

On va reverse GETFLAG directement. On sort CUTTER ! 

![Voilà a quoi ressemble GETFLAG](https://github.com/bhm-heddy/42project_snowcrash/blob/master/level14/Ressources/full_getflag.png)
Les fonctions en bleues sont des protections anti reverse et anti Hijackings

La fonction en jaune effectue le `getuid()` permettant de savoir quel flag return.

La fonction en verte est donc justement la fonction qui return le flag du level14

![](https://github.com/bhm-heddy/42project_snowcrash/blob/master/level14/Ressources/flag14.2.png)

On voit le flag mais il est chiffré, et la fonction `ft_des` doit déchiffrer le flag à l'aide du chiffrement symétrique [Data Encryption Standard](https://en.wikipedia.org/wiki/Data_Encryption_Standard).

Dans une instruction de la fonction `ft_des` on retrouve la string "0123456"
![](https://github.com/bhm-heddy/42project_snowcrash/blob/master/level14/Ressources/ft_des.png)

La clé de déchiffrement doit être "0123456". On pourrait déchiffrer nous même la clé mais vu que le programme le fait, on va se placer juste après l'appel à `ft_des` et regarder la variable. 

![](https://github.com/bhm-heddy/42project_snowcrash/blob/master/level14/Ressources/jump.png)

![](https://github.com/bhm-heddy/42project_snowcrash/blob/master/level14/Ressources/flag!.png)

Et voila notre 

**TOKEN=7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ**
