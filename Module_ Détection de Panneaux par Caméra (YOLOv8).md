
# Module: Détection de Panneaux par Caméra (YOLOv8)

Ce module est responsable de la détection et de la reconnaissance des panneaux de signalisation de limitation de vitesse à partir de flux vidéo ou d'images, en utilisant le modèle de Deep Learning YOLOv8.

## Contenu du Module

*   **`yolov8_model/`**: Contient les poids des modèles YOLOv8 entraînés (`.pt` files) et les fichiers de configuration (`.yaml`).
*   **`scripts/`**: Scripts Python pour l'inférence en temps réel, le traitement des vidéos, et l'application du modèle sur de nouvelles données.
    *   `run_detection.py`: Script principal pour exécuter la détection sur une source vidéo (webcam, fichier vidéo).
*   **`data_preparation/`**: Scripts et instructions pour la préparation des datasets d'entraînement, incluant l'annotation (ex: avec Roboflow) et l'augmentation de données.

## Fonctionnalités

*   Détection en temps réel des panneaux de limitation de vitesse (standard, fin de limitation, travaux).
*   Utilisation de YOLOv8n/s pour un équilibre optimal entre précision et vitesse d'inférence.
*   Extraction des informations clés des panneaux détectés (type de panneau, vitesse, score de confiance).
*   Préparation des données pour l'entraînement de modèles de détection d'objets.

## Utilisation

### Entraînement (si vous souhaitez entraîner votre propre modèle)

1.  **Préparer votre dataset**: Suivez les instructions dans `data_preparation/` pour annoter vos images et générer un fichier `dataset.yaml`.
2.  **Lancer l'entraînement**: Utilisez le script d'entraînement YOLOv8 (souvent via la bibliothèque `ultralytics`):
    ```bash
    yolo train model=yolov8n.pt data=data_preparation/dataset.yaml epochs=100 imgsz=640
    ```
    Placez le modèle entraîné (`best.pt`) dans `yolov8_model/`.

### Exécution de la Détection

Pour exécuter la détection sur un flux vidéo ou un fichier:

```bash
python scripts/run_detection.py --source 0  # Pour la webcam
# ou
python scripts/run_detection.py --source path/to/your/video.mp4
```

## Dépendances Spécifiques

*   `ultralytics`
*   `opencv-python`
*   `Pillow`
*   `numpy`

Assurez-vous que ces dépendances sont installées dans votre environnement Python (`pip install -r ../requirements.txt`).


