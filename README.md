# TP de Physique Numérique : Dynamique Quantique
Les tp de physique numérique pour modéliser et utiliser l'informatique dans la physique

## Installation 

Pour installer le dossier, copier dans la console git 
```sh
git clone https://github.com/Rockinfox91/phys_num_quantique.git
```

puis lancer Jupyter Notebook

# Partie 1 - Etats stationnaires

Dans un premier temps, on pourra considérer uniquement les états stationnaires du problème, ce qui permettra de traiter d’abord la discrétisation spatiale.

## Vérification de la validité du modèle numérique

Le but ici est de modéliser numériquement des états stationnaires avec un potentiel indépendant du temps.

On va alors pour voir par exemple faire l'application numérique avec des potentiels : 

- Nul (qui représente donc un puit de potentiel infini aux limites)
- Harmonique (en x²)

Ce qui nous permet de les comparer aux résultats théorique et de vérifier la validité de la modélisation numérique.

### Puit de potentiel infini

![](/etat_stationnaire/document/psi_fonction_de_x_puit_infini_n10.png?raw=true)
![](/etat_stationnaire/document/psi_fonction_de_x_puit_infini_n100.png?raw=true)

### Potentiel Harmonique

![](/etat_stationnaire/document/psi_fonction_de_x_harmonique_n10.png?raw=true)
![](/etat_stationnaire/document/psi_fonction_de_x_harmonique_n100.png?raw=true)

## Tentative avec d'autres potentiels plus compliqués

Ensuite, on tente des potentiels plus complexes tel que :

- Le double puit de potentiel
- Potentiel périodique
etc...

On peut voir les résultats des rendus dans le dossier document.

# Partie 2 - Évolution temporelle dans le cas d’un puits infini et d’un potentiel harmonique

On étudie dans cette partie l’évolution temporelle de la fonction d’onde $\Psi(x, t)$ d’un état décrit par une fonction d’onde initiale $\Psi(x, 0)$.

On considèrera d’abord le puits infini et le potentiel harmonique, pour lesquelles les solutions analytiques exactes sont connues, afin de vérifier l’évolution temporelle obtenue numériquement.

## Algorithme d'Euler

Ici, on utilise l'algorithme d'Euler explicite pour obtenir l'évolution temporelle de la fonction d'onde. Cet algorithme, bien que simple à utiliser, n'est pas très efficace.

Lors de la partie 1, on utilisait un Hamiltonien à valeurs réelles, ici nous sommes obligés d'utiliser des valeurs complexes.

On obtient pour l'algorithme d'Euler :

$$ \Psi(x,t+1) = \Psi(x,t) + dt\cdot f(\Psi(x,t)) $$

avec

$$ f(\Psi(x,t)) = -iH\Psi(x,t) $$

### Puit de potentiel inifini

#### Etat stationnaire

![](/docs/tempo/psi_fonction_de_x_euler_etat_statio0_m10000_duree_10.jpeg?raw=true)
![](/docs/tempo/psi_fonction_de_x_euler_etat_statio0_m100000_duree_10.jpeg?raw=true)

#### Paquet d'onde gaussien

![](/docs/tempo/psi_fonction_de_x_euler_gaussienne_m10000_duree_1000.jpeg?raw=true)

![](/docs/tempo/psi_fonction_de_x_euler_gaussienne_m10000_duree_2000.jpeg?raw=true)

![](/docs/tempo/psi_fonction_de_x_euler_gaussienne_m100000_duree_10000.jpeg?raw=true)

![](/docs/tempo/anim.gif?raw=true)

On remarque bien ici que la quantité de calcul demandée est énorme, et ce même pour un temps très court. On va donc tenter une nouvelle méthode : l'algorithme de Runge-Kutta d'ordre 4

## Algorithme de Runge-Kutta d'ordre 4

Pour cet algorithme, on a :

$$ \Psi(x,t+1) = \Psi(x,t) + dt\cdot (\frac{1}{6}k_1 + \frac{1}{3}k_2 + \frac{1}{3}k_3 + \frac{1}{6}k_4)$$

avec :

$$ k_1 = f(\Psi(x,t))$$

$$ k_2 = f(\Psi(x,t) + \frac{1}{2} dt\cdot k_1)$$

$$ k_3 = f(\Psi(x,t) + \frac{1}{2} dt\cdot k_2)$$

$$ k_4 = f(\Psi(x,t) + dt\cdot k_3)$$

On obtient alors :

![](/docs/tempo/anim_gauss_pot_nul_séparé.gif?raw=true)

On remarque bien ici que l'algorithme de Runge-Kutta d'ordre 4 est bien plus précis, et beaucoup moins
demandant en ressources.

# Sources : 

