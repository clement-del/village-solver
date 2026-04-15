# 🧩 Puzzle Solver 7x7 - Agentique & Vision

Projet de résolution automatisée d'un casse-tête géométrique par intelligence artificielle. Ce système utilise la vision par ordinateur pour interpréter les plans de montage et un algorithme de backtracking optimisé pour trouver les solutions en temps réel.

---
# Règles du Jeu
- Retirez du plateau les 9 éléments de ville ainsi que le réverbère.
- Placez le réverbère dans un des 13 trous du plateau en bois.
- Le jeu va ensuite consister à réussir à replacer tous les éléments de ville sur le plateau en un minimum de temps.

  
## 📖 Concept & Règles du Jeu

Le casse-tête se compose de deux éléments principaux :

1.  **Le Support (49-squares-frame) :** * Une grille de **7x7 cases** (49 carrés au total).
    * **13 positions spécifiques** identifiées par des cercles sur le support.
    * Une de ces positions doit impérativement accueillir la pièce n°10 au démarrage.

2.  **Les Pièces (10-pieces-shape) :**
    * **10 pièces uniques** numérotées de 1 à 10.
    * Chaque pièce possède une surface définie (ex: n°1 = 8sq, n°9 = 2sq).
    * La somme totale des surfaces des 10 pièces est de **49sq**, ce qui signifie qu'une solution valide remplit parfaitement la grille sans aucun espace vide.
    * La **pièce n°10** est le "pivot" : elle n'occupe qu'un seul carré et doit être placée sur l'un des cercles du support.

---

## 🚀 Stratégie de Résolution

L'agent de résolution utilise un algorithme de **Backtracking avec Élagage (Pruning)** :

1.  **Initialisation :** Placement de la pièce n°10 sur la coordonnée cible (choisie parmi les cercles).
2.  **Ordonnancement (Heuristique de Contrainte) :** Les pièces sont triées par taille décroissante. L'algorithme tente de placer les plus volumineuses (n°1, n°2, n°3) en premier pour réduire drastiquement l'arbre des possibilités dès le début.
3.  **Exploration Récursive :** * Recherche de la première case vide disponible (balayage haut-gauche vers bas-droite).
    * Test de chaque pièce restante avec toutes ses rotations (0°, 90°, 180°, 270°) et symétries miroirs.
4.  **Élagage :** Si un placement crée une zone vide isolée dont la taille est incompatible avec les pièces restantes, la branche est immédiatement abandonnée (Backtrack).

---

## 🖥️ Interface Utilisateur (UI/UX)

L'application propose une interface interactive divisée en deux zones :

### A. La Grille de Visualisation
* Rendu 2D dynamique montrant le placement des pièces en temps réel.
* Code couleur distinct pour chaque numéro de pièce pour une identification immédiate.

### B. La Zone de Suivi (Monitoring)
Pour observer "l'intelligence" à l'œuvre, un tableau de bord affiche :
* **Calculs effectués :** Compteur total des tentatives de placement de pièces.
* **Nombre de Backtracks :** Indicateur de la difficulté du puzzle (nombre d'impasses rencontrées).
* **Vitesse de traitement :** Nombre de positions testées par seconde.
* **Profondeur actuelle :** Nombre de pièces (X/10) placées avec succès dans la branche d'exploration actuelle.

---

## 🛠️ Stack Technologique

| Domaine | Technologie | Rôle |
| :--- | :--- | :--- |
| **Vision** | OpenCV + NumPy | Détection des contours et numérisation des pièces/grilles. |
| **Backend** | Python 3.10+ | Moteur logique et algorithme de backtracking. |
| **Frontend** | Streamlit ou React | Interface de dashboard et monitoring temps réel. |
| **Communication** | WebSockets | Transmission fluide des données de calcul vers l'UI. |
| **Performance** | Numba (JIT) | Accélération du moteur de calcul si nécessaire. |

---

## 📝 Utilisation

1.  **Scan :** Photographier le support et les pièces séparément.
2.  **Configuration :** Sélectionner via l'interface le cercle où poser la pièce 10.
3.  **Résolution :** Lancer le moteur et observer la progression dans la zone de suivi jusqu'à l'obtention de la grille complète.
