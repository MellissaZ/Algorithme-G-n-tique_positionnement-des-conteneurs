
# Modalisation du  problème de positionnement de  conteneurs  et l’algorithme génétique
##### Dans ce projet, nous nous intéressons à la description et la modalisation du problème  de positionnement de conteneurs  dans un parc à conteneurs en utilisant l’algorithme génétique
### Description du problème
##### Nous considérons la cour de stockage où résident les différents conteneurs du port maritime. On s’intéresse aux différentes catégories de conteneurs en supposant qu'ils ne sont pas mélangés aux autres catégories (de différents contenue) de conteneur dans la cour de stockage. Cela sous-entend que la cour de stockage est divisée en zones qui sont réservées chacune à une catégorie de conteneur précise, nous considérons aussi que des conteneurs de différents types (différents dimensions)  peuvent être stockés ensemble (dans la même zone). Ce procédé permet d'accélérer les opérations de chargement des navires et des trains, et de diminuer les temps d'attente des camions.Afin de résoudre le problème de positionnement de conteneurs dans un parc à conteneurs, nous utilisons des méta-heuristiques afin de trouver la solution optimale,Tel qu’on va appliquer l’algorithme génétique pour l’optimisation du temps nécessaire pour effectuer les chargements et les déchargements des navires.Dans les méthodes de résolution que nous proposons, nous considérons ces quatre Hypothèses suivantes :
<ol>

##### <li>On tient compte des différences de taille entre les conteneurs, et on stocke dans chaque pile uniquement des conteneurs de mêmes dimensions.</li>
##### <li>Des conteneurs sont de même catégorie s'ils ont le même contenu et de même type s'ils ont la même dimension.</li>
##### <li> On suppose que les conteneurs sont numérotés suivant leurs ordres d'arrivée.</li>
##### <li> On considère que les piles sont numérotées de sorte que deux piles adjacentes aient des numéros successifs.</li>
</ol>


### Modalisation  
##### Résoudre le problème de positionnement des conteneurs revient à résoudre le problème de coloration de graphe, et pour cela nous introduisons un graphe non orienté G (K,T,R)=(V,E), Construit à partir d'une instance quelconque du problème de positionnement de conteneurs.
##### K : L'ensemble des conteneurs.
#####                        Où        T : Tableau de la date de départ de chaque conteneur.
##### R : Tableau de  la taille de chaque conteneur.
##### Le graphe G (K,T,R) est construit de la manière suivante. Un sommet du graphe correspond à un conteneur. Pour simplifier les notations, on utilisera l'indice k pour désigner à la fois un conteneur et le sommet du graphe qui lui correspond. On a une arête entre deux sommets k et k0 si et seulement si les conteneurs correspondants ne peuvent pas être stockés dans une même pile. En d'autres termes, si Rₖ ≠ Rₖ₀, car deux conteneurs qui ont des dimensions inégales ne peuvent pas être placés dans une même pile.
<img width="100%" height="auto"/>![](graphe.png)

### Critères de développement de l’algorithme génétique
##### L’algorithme consiste à positionner des conteneurs dans les piles des zones de stockage. Pour développer l’algorithme génétique pour notre étude, nous prenons en compte les contraintes suivantes :
<ol>

##### <li>	Chaque conteneur est affecté à un seul emplacement.</li>
##### <li>	Plusieurs conteneurs ne sont pas simultanément affectés à un même emplacement.</li>
##### <li>	Dans chaque pile, sont stockés uniquement des conteneurs qui ont les mêmes dimensions (même type).</li>
##### <li>	Dans chaque zone, sont stockés uniquement les conteneurs de même catégorie.</li>
##### <li>	Le nombre de piles exploitées ne doit pas dépasser le nombre de pile disponibles.  </li> 
##### <li>	Chaque conteneur a une dimension (10 pieds, 20 pieds et 30 pieds) et une catégorie selon le contenu (produit 1, produit 2 et produit 3).</li>
##### <li>	On a trois zones chaque zone reçoit une catégorie de conteneurs (zone 1 pour produit 1, zone 2 pour produit 2 et zone 3 pour produit 3)</li>
##### <li>	Le nombre de pile de chaque zone est fixé à 24 piles (8 piles pour chaque type de conteneurs dans chaque zone).</li>
##### <li>	Chaque pile à une hauteur maximale si la pile est pleine on ne peut pas insérer un conteneur, on passe alors à la pile suivante de même type.</li>
##### <li>	Le remplissage de chaque pile se fait de bas en haut sans sauter aucun emplacement intermédiaire </li>
</ol>

### Modalisation de l’algorithme génétique 
##### L'algorithme génétique que nous proposons pour la résolution du problème de positionnement  de conteneurs dans un parc à conteneurs comprend principalement quatre étapes qui sont : la création d'une population initiale, la sélection d'une partie de cette population, l'application de croisements entre les individus sélectionnés, et la mutation des individus résultats du croisement
<ol>

#### <li>Création de la population initiale</li>
##### Dans notre algorithme génétique, chaque individu de la population est une solution Valide du problème de positionnement de conteneurs. Par conséquent, nous représentons chaque individu sous forme d'un tableau qui a deux lignes et dont le nombre de colonnes est égal au nombre de conteneurs à positionner. Les conteneurs sont notés dans la première ligne (Les conteneurs sont représentés dans le tableau selon leurs ordres d’arrivée)  alors que les piles sont notées dans la deuxième ligne

#### <li>La taille de la population à manipuler</li>
##### La taille de la population initiale est laissée à l'appréciation du programmeur, selon le problème à résoudre. Dans notre cas une taille de 20 ou 30 individus sera suffisante.<br>Ensuite, libre à l’utilisateur de modifier la taille de la population initiale si les solutions trouvées ne sont pas satisfaisants dans on a autorisé un intervalle de 5 à 30 individus.

#### <li> La fonction Fitness </li>
##### Le résultat fournit par la fonction fitness pour une solution donnée permet de décider si l’individu sera sélectionné ou non. La valeur attribuée à chaque chromosome représente donc son aptitude ou sa capacité d’adaptation à l'environnement, dans notre cas la valeur du fitness est le nombre de conteneurs mal positionnés dans le différentes piles de la zone (un conteneurs mal positionné est un conteneur placé sur un autre conteneur qui a une date de départ plus proche) qui vont causer plusieurs remaniement lors de déchargement des conteneurs et ça fait une perte du temps et ça augmente les mouvement au niveau de la cour de stockage(les aller retours des camion , portique...) .Notre algorithme génétique détermine les solutions qui ont les valeurs de fitness les plus petites parmi l'ensemble des solutions possibles. Cette méthode permet de s'assurer que les individus performants seront conservés, alors que les individus peu adaptés seront progressivement éliminés de la population

#### <li> La sélection  </li>
##### La sélection est la première phase de renouvellement d'une population. Comme son nom l'indique, elle permet de sélectionner les individus qui vont donner naissance à la descendance d'une génération. Ils existent différentes méthodes de sélection (voir chapitre 2), nous allons appliquer à notre algorithme génétique la méthode élitiste qui permet de mettre en avant les meilleurs individus de la population tel qu’on sélectionne la moitié de la population (  N/2 ) en respectant la contrainte de sélectionner les meilleurs individus

#### <li> Le croisement    </li>
##### Dans un algorithme génétique, l'opérateur croisement sert à créer de nouveaux individus (appelés enfants), en combinant des parties d'autres individus (appelés parents). Il existe différentes méthodes de croisement (voir chapitre 2). Cependant, nous utilisons la méthode de croisement en un point, car le croisement en deux points ainsi que les autres méthodes nécessitent plus de corrections qui sont en rapport avec les contraintes de positionnement des conteneurs suivant leur catégorie(dimension) et la disponibilité de l’espace dans la pile. Avant le croisement, on choisit aléatoirement un nombre réel (x) compris entre 0 et 100. Si x est supérieur à la probabilité de croisement (pc), alors on applique le croisement sinon on passe à l’étape suivante. Lors d'un croisement, on choisit aléatoirement deux parents parmi les individus sélectionnés et on sélectionne aléatoirement un point de section. Après cela, on intervertit les parties des deux parents qui sont de part et d'autre du point de section. Ainsi on crée deux enfants, voir figure P5.6.4. Ensuite, on vérifie s'ils sont valides, en d'autres termes s'ils satisfont toutes les contraintes. S'il y a des contraintes qui sont violées, on effectue les corrections nécessaires.

#### <li> La mutation   </li>
##### La mutation sert à diversifier les générations afin d'éviter une convergence prématurée vers un optimum local. Dans notre algorithme génétique, elle est effectuée à la fin de chaque itération en fonction d'une probabilité que l'on nomme pm. Ainsi, à la fin de chaque itération, on choisit aléatoirement un nombre réel (rm). Si rm < pm, alors on fait une mutation. Pour ce faire, on choisit le meilleur individu de la population et on choisit aléatoirement deux entier a et b  entre 0 et le nombre de colonne de l’individu (l’individu dans notre cas c’est un tableau à deux lignes) pour faire une permutation entre la colonne de l’indice a  et celle de l’indice b (on fait la permutation que dans la 2eme ligne du tableau). Ensuite, on vérifie si l’individu après mutation est valide, en d’autres termes s’il satisfait toutes les contraintes. S’il y a des contraintes qui sont violées, on effectue les corrections nécessaires, voir figure P4.6.5. La procédure de vérification et de correction est la même que celle appliquée dans le croisement.

#### <li> Application de l’Algorithme génétique   </li>
##### Ici nous expliquons l’application de notre algorithme génétique et pour se faire, nous commençons d'abord par chercher les bonnes valeurs des paramètres utilisés dans cet algorithme. Chaque paramètre est traité individuellement, en fixant les autres paramètres, et en le faisant varier. Les résultats obtenus sont marqués dans le tableau suivant :
<img width="50%" height="auto"/>![](T.png)

##### On applique notre algorithme génétique jusqu’à avoir les deux meilleurs individus de notre population, ensuite on prend le meilleur individu entre ces deux derniers comme meilleur solution (solution optimale) pour notre problématique. <br>On applique l’algorithme génétique sur les trois zones et chaque zone aura sa propre solution  

### Application
##### Cet application est réalisée avec Java,JavaFx et MySQL.
![](V.mp4)
