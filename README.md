# GNextOmnia

GNextOmnia est une application logicielle universelle visant à améliorer les performances des jeux vidéo en réduisant la latence et en augmentant les FPS. 

## Fonctionnalités principales
- Augmentation de la fluidité des jeux (élimination des micro-lags, frame generation, interpolation)
- Compatible avec toutes les configurations PC (modestes et haut de gamme)
- Interface graphique personnalisable via **Glade**
- Architecture modulaire permettant l'ajout de nouvelles fonctionnalités

## Technologies utilisées
- **Langage** : C++
- **Interface graphique** : GTK 3, GTKMM 3, Glade
- **Compilation** : MSYS2, CMake
- **Gestion du code** : GitHub
- **Optimisations** : OpenGL Compute Shader, Vulkan/OpenCL (prévu)
- **Configuration** : JSON

- Voici la section mise à jour pour le README de **GNextOmnia** concernant la détection automatique de l'API graphique et l'activation de la méthode appropriée de **Frame Generation** :

---

## Frame Generation avec Compute Shaders

Le **Frame Generation** dans **GNextOmnia** utilise des **Compute Shaders** pour améliorer la fluidité des jeux en générant des images intermédiaires. Cette fonctionnalité est compatible avec **OpenGL**, **Vulkan** et **DirectX** (9, 9+, 10, 11, 12) grâce à une architecture flexible et modulaire. **GNextOmnia** détecte automatiquement l'API graphique utilisée sur le système et choisit la méthode de génération de frames la plus adaptée.

### Fonctionnement

Le principe de base du **Frame Generation** repose sur l'**estimation du mouvement** (Motion Estimation) et le **mélange** (Blending) des images pour générer des frames intermédiaires entre celles existantes. Cela permet d'augmenter le nombre d'images par seconde (FPS) et de rendre l'animation plus fluide. Voici un résumé du processus :

1. **Capture des images** : 
   Le programme capture deux frames successives provenant du rendu du jeu.

2. **Estimation du mouvement** :
   Un **Compute Shader** est utilisé pour estimer le mouvement des pixels entre les deux frames successives, en calculant la direction et l'intensité du déplacement des objets à l'écran.

3. **Génération de frames intermédiaires** :
   Grâce à l'estimation du mouvement, des images intermédiaires sont générées en interpolant les frames existantes, ce qui améliore la fluidité de l'animation.

4. **Blending des images** :
   Les images intermédiaires sont combinées avec les images originales pour créer des transitions fluides, réduisant les artefacts visuels.

5. **Affichage de l'animation fluide** :
   Les images générées sont envoyées pour être affichées à l'écran, augmentant ainsi la fluidité du rendu.

### Détection Automatique de l'API Graphique

**GNextOmnia** détecte automatiquement l'API graphique utilisée par le système et adapte la méthode de **Frame Generation** en conséquence. Cela évite à l'utilisateur de devoir sélectionner manuellement l'API et garantit une expérience optimale.

1. **OpenGL** :
   Si **OpenGL** est détecté, le système initialise les **Compute Shaders** pour générer des frames intermédiaires en utilisant les capacités de **Compute Shaders** d'OpenGL 4.3 et plus.

2. **Vulkan** :
   Si **Vulkan** est utilisé, **GNextOmnia** active les **Compute Shaders** en Vulkan pour générer des frames intermédiaires avec des performances améliorées sur les GPU récents.

3. **DirectX** :
   - Si **DirectX 11** ou **DirectX 12** est détecté, le système utilise les **Compute Shaders** de DirectX pour générer les images intermédiaires.
   - Si **DirectX 9** ou **DirectX 10** est utilisé, le système utilise une méthode alternative basée sur les **Pixel Shaders** ou **Vertex Shaders** pour générer les images intermédiaires.

### Implémentation

Le système utilise une approche modulaire pour gérer différentes API graphiques. Voici comment il fonctionne :

- **Technologies utilisées** : Compute Shaders pour Vulkan, DirectX (10/11/12), et OpenGL.
- **Abstraction de l'API** : Une interface commune permet de gérer différentes API graphiques, offrant ainsi la possibilité d'utiliser Vulkan, OpenGL ou DirectX en fonction des préférences et de la configuration du système.
- **Performances** : Le **Frame Generation** est optimisé pour fonctionner efficacement sur différents types de matériel, des configurations basiques aux systèmes de haute performance.

### Options de configuration

Dans **GNextOmnia**, cette fonctionnalité peut être activée ou désactivée via l'interface graphique. L'utilisateur n'a pas besoin de spécifier manuellement l'API graphique, car **GNextOmnia** la détecte automatiquement. Toutefois, l'utilisateur peut choisir d'activer ou de désactiver certaines options de **Frame Generation**.

---

# GNext Omnia - Latency Reducer

##  Réduction de la Latence avec GNext Omnia
Le **Latency Reducer** de GNext Omnia est conçu pour diminuer la latence entre les entrées utilisateur (clavier/souris) et l'affichage à l'écran. Cette fonctionnalité optimise la communication entre le CPU, le GPU et les périphériques d'entrée pour améliorer la réactivité des jeux. Elle est compatible avec les technologies de **Frame Generation** et **Upscaling**.

##  Fonctionnement
Le système de réduction de latence fonctionne en optimisant différents aspects de la pipeline de rendu et du traitement des entrées :

1. **Optimisation du buffering CPU/GPU** : Réduction du buffering d'image pour un affichage plus réactif.
2. **Input Polling Ultra-Rapide** : Fréquence d'interrogation des entrées augmentée pour une meilleure précision.
3. **Synchronisation direct des entrées et du rendu** : Assure que les actions de l'utilisateur sont prises en compte à la frame la plus récente.
4. **Adaptation à l'API Graphique** :
   - **OpenGL** : Optimisation du swap buffer et des frames en attente.
   - **Vulkan** : Utilisation avancée des synchronisations CPU-GPU.
   - **DirectX (9, 10, 11, 12)** : Gestion des files de rendu pour minimiser la latence.

##  Modes de Fonctionnement
- **Ultra Low Latency 🔥** : Mode extrême pour un rendu sans file d'attente, idéal pour les jeux compétitifs.
- **Balanced Mode ⚖** : Un compromis entre latence réduite et fluidité.
- **Performance Mode 🎮** : Optimisation générale pour réduire la latence sans impacter la stabilité.

##  Intégration avec GNext Omnia
Le module de réduction de latence fonctionne de manière transparente avec les autres modules de GNext Omnia, notamment **Frame Generation** et **Upscaling**. Il garantit une synchronisation optimale pour maximiser la fluidité tout en conservant une faible latence.
