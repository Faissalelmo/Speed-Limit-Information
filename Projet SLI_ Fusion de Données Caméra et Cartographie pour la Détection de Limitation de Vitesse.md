# 🚦 Projet SLI: Fusion de Données Caméra et Cartographie pour la Détection de Limitation de Vitesse

## Table des Matières
1. [Objectif du Projet](#objectif-du-projet)
2. [Modules Utilisés](#modules-utilisés)
3. [Structure du Dépôt](#structure-du-dépôt)
4. [Dépendances](#dépendances)
5. [Étapes pour l'Exécuter](#étapes-pour-lexécuter)
6. [Résultats et Démonstrations](#résultats-et-démonstrations)
7. [Code Complet et Datasets](#code-complet-et-datasets)

## 1. Objectif du Projet
Ce projet de fin d'études vise à améliorer la fiabilité de la détection des limitations de vitesse dans les véhicules en combinant deux sources d’information : la détection visuelle par caméra et les données issues de la cartographie numérique. Le système développé repose sur une architecture modulaire, intégrant des algorithmes de vision embarquée, de map-matching, et de fusion décisionnelle. L’approche proposée permet de pallier les limites de chaque méthode lorsqu’elles sont utilisées de manière isolée, en assurant une meilleure précision et une meilleure couverture dans la détection des vitesses maximales autorisées. L'objectif est d'atteindre une fiabilité supérieure à 97% pour le système SLI (Speed Limit Information).

## 2. Modules Utilisés
Le projet est structuré autour de plusieurs modules principaux, chacun ayant un rôle spécifique dans le processus de détection et de fusion des données de limitation de vitesse:

*   **`camera_detection`**: Contient le code et les modèles liés à la détection des panneaux de signalisation par vision par ordinateur (YOLOv8).
*   **`map_detection`**: Gère l'acquisition, le traitement et le recalage des données cartographiques (OpenStreetMap, OSRM) et GPS.
*   **`fusion_algorithm`**: Implémente l'algorithme de fusion des données provenant de la caméra et de la carte pour une estimation fiable de la limitation de vitesse.
*   **`common_utils`**: Regroupe les utilitaires et fonctions partagées par les différents modules.

## 3. Structure du Dépôt
```
. 
├── camera_detection/
│   ├── yolov8_model/           # Modèles YOLOv8 entraînés et configurations
│   ├── scripts/                # Scripts pour l'inférence et le traitement vidéo
│   └── data_preparation/       # Scripts pour la préparation des datasets (annotation, augmentation)
├── map_data_processing/
│   ├── osrm_integration/       # Code pour l'intégration avec OSRM (Map-Matching)
│   ├── osm_data/               # Gestion des données OpenStreetMap (téléchargement, stockage)
│   └── gps_processing/         # Traitement des données GPS brutes
├── fusion_algorithm/           # Algorithmes de fusion et logique décisionnelle
├── common_utils/               # Fonctions utilitaires partagées
├── data_and_models/            # Emplacement pour les datasets bruts, modèles pré-entraînés, etc.
├── docs/                       # Documentation additionnelle, rapports, présentations
├── results/                    # Images et vidéos des résultats de détection et de fusion
├── README.md                   # Ce fichier
├── requirements.txt            # Liste des dépendances Python
└── .gitignore                  # Fichier pour ignorer les fichiers non nécessaires dans Git
```

## 4. Dépendances
Ce projet nécessite les dépendances Python suivantes. Il est recommandé de créer un environnement virtuel pour les installer:

```bash
pip install -r requirements.txt
```

Les principales bibliothèques utilisées incluent:
*   `ultralytics` (pour YOLOv8)
*   `opencv-python`
*   `Pillow`
*   `numpy`
*   `pandas`
*   `geopandas`
*   `shapely`
*   `folium`
*   `PyQt5` (pour l'interface graphique)
*   `python-can` (pour la simulation CAN)
*   `requests` (pour les requêtes API)
*   `python-dotenv`
*   `gpxpy`
*   `scikit-learn`
*   `matplotlib`
*   `seaborn`

Pour le module de traitement cartographique, OSRM doit être exécuté localement, idéalement via Docker. Les instructions pour sa mise en place sont détaillées dans le `map_data_processing/README.md`.

## 5. Étapes pour l'Exécuter

### 5.1. Configuration de l'Environnement
1.  **Cloner le dépôt GitHub**:
    ```bash
    git clone [URL_DU_DEPOT]
    cd [NOM_DU_DEPOT]
    ```
2.  **Créer et activer un environnement virtuel** (recommandé):
    ```bash
    python -m venv venv
    source venv/bin/activate  # Linux/macOS
    # ou
    .\venv\Scripts\activate   # Windows
    ```
3.  **Installer les dépendances Python**:
    ```bash
    pip install -r requirements.txt
    ```
4.  **Mettre en place OSRM (via Docker)**:
    Suivez les instructions dans `map_data_processing/README.md` pour lancer le serveur OSRM localement.

### 5.2. Préparation des Données et Modèles
*   **Modèles YOLOv8**: Les modèles pré-entraînés ou vos propres modèles entraînés doivent être placés dans `camera_detection/yolov8_model/`.
*   **Données OSM**: Le système téléchargera automatiquement les données OSM nécessaires via l'API Overpass. Assurez-vous d'avoir une connexion internet fonctionnelle lors de la première exécution.
*   **Traces GPS**: Placez vos fichiers `.gpx` de traces GPS dans `map_data_processing/gps_processing/`.

### 5.3. Exécution du Projet
Le projet est conçu pour être exécuté via un script principal qui orchestre les différents modules. Des exemples de scripts d'exécution seront fournis dans les dossiers de chaque module.

*   **Exécution du module de détection caméra**:
    ```bash
    python camera_detection/scripts/run_detection.py 
    ```
*   **Exécution du module de traitement cartographique**:
    ```bash
    python map_data_processing/run_map_processing.py 
    ```
*   **Exécution du système de fusion**:
    ```bash
    python fusion_algorithm/run_fusion.py
    ```

Des paramètres supplémentaires peuvent être spécifiés (voir les `README.md` spécifiques à chaque module pour plus de détails).

## 6. Résultats et Démonstrations
Ce dossier contient des images et des vidéos illustrant les résultats obtenus lors des tests du projet. Vous y trouverez des exemples de:

*   Détection de panneaux de signalisation en temps réel par YOLOv8.
*   Visualisation du recalage cartographique (Map-Matching) des traces GPS sur OpenStreetMap.
*   Démonstrations de la fusion des données caméra et carte, et de l'affichage des limitations de vitesse.

**Accéder aux résultats**: [[Lien vers le dossier `results](https://drive.google.com/drive/folders/1RfBbEmmLGVCvTwhYuqfYjoiG9TB6Wwa_?usp=drive_link)]

## 7. Code Complet et Datasets
Le code complet du projet, incluant les datasets d'entraînement, les notebooks Jupyter, et les scripts détaillés, est disponible dans le dossier Google Drive suivant:

👉 [**[Le lien vers le projet SLI](https://drive.google.com/drive/folders/1oTisFENqo5xwP31eMjg7Vhcya6iwTsfb?usp=drive_link)**]

Ce lien vous donnera accès à l'intégralité des ressources du projet, y compris les données brutes et les modèles spécifiques.

## 📊 Features

- ✅ Real-time detection of speed limit signs
- ✅ GUI with PyQt5
- ✅ Distance estimation between sign and camera
- ✅ Speed quality alert
- ✅ Works on webcam or video input

## 🔮 Future Improvements

- Integrate vehicle's real speed from GPS or CAN bus
- Add voice alerts for over-speeding
- Expand to detect other traffic signs (Stop, Yield, etc.)
- Deploy on edge devices (Jetson Nano, Raspberry Pi)

## 👤 Author

Developed by **Faissal Elmokaddem**  
📧 Contact: faissal.elmokaddem@gmail.com  
🔗 LinkedIn: [linkedin.com/in/faissal-elmokaddem](https://linkedin.com/in/faissal-elmokaddem)  
💻 GitHub: [github.com/FaissalElmokaddem](https://github.com/FaissalElmokaddem)

## 📜 License

This project is licensed under the MIT License.

---

🚗 *"Driving safely with AI-powered vision."*
