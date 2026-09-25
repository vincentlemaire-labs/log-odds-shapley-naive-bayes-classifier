Ce projet est piloté par un notebook principal (l'orchestrateur)
qui exécute en boucle une série de sous-notebooks
pour chaque jeu de données, avant d'agréger les résultats globaux.

### 🧠 L'Orchestrateur : **`RunAllDatasets_and_CriticalDiagrams.ipynb`** : 
 
C'est le point d'entrée du projet. Pour chaque dataset défini dans la liste, il lance séquentiellement les sous-notebooks. Une fois tous les datasets traités, il compile les résultats dans un tableau récapitulatif et génère un **Critical Difference Diagram** (Test de Friedman & Nemenyi) pour comparer globalement les méthodes.

### ⚙️ Les Sous-Notebooks (exécutés par l'orchestrateur)
1. **`MakeCI-ponderees-files.ipynb`** :
   - ** Entraîne un classifieur Khiops SNB [1]
   - ** Génère pour chaque dataset les valeurs des 'Conditional Info' pondérées (w * log(P[D|C)) ET les log(P(D)) - en utilisant  [1]
   - ** C'est ce notebook qui crée les 10 folds stratifiés pour chaque dataset
   
2. **`ComputeShapleyValues.ipynb`** :
   - ** Génère pour chaque dataset les valeurs de Shapley, sur les 10 folds stratifiés produit par le notebook précédent, en utilisant  [1]

3. **`kppv.ipynb`** :
   - ** A l'aide des représentations créées par les 2 notebooks précédents
   - ** Recherche des plus proches voisins et calcul des prédictions $k$-PPV en utilisant les 3 distances de l'article
   - ** Évaluation des métriques de performance.

Il est possible d'ajouter / remplacer des datasets dans **`RunAllDatasets_and_CriticalDiagrams.ipynb`** pour avoir de nouveaux résultats.