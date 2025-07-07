
# Module: Traitement des Données Cartographiques (MAP)

Ce module gère l'acquisition, le traitement et le recalage des données cartographiques (OpenStreetMap) et des données GPS pour déterminer la limitation de vitesse applicable en fonction de la position du véhicule.

## Contenu du Module

*   **`osrm_integration/`**: Contient le code et les scripts pour l'intégration avec le serveur OSRM (Open Source Routing Machine) pour le Map-Matching.
*   **`osm_data/`**: Gère le téléchargement, le stockage local (SQLite) et la manipulation des données OpenStreetMap via l'API Overpass.
*   **`gps_processing/`**: Scripts pour le traitement des traces GPS brutes (`.gpx` files) et leur préparation pour le Map-Matching.

## Fonctionnalités

*   Acquisition des données GPS et recalage cartographique précis en utilisant OSRM.
*   Téléchargement dynamique des données OpenStreetMap (OSM) pour la zone de conduite actuelle.
*   Extraction des limitations de vitesse et des types de routes à partir des données OSM.
*   Calcul d'un score de fiabilité pour les données cartographiques.
*   Simulation de la communication avec des serveurs d'authentification (STLA) et de données cartographiques (MAP).

## Utilisation

### Mise en place du serveur OSRM (via Docker)

Pour que le module de traitement cartographique fonctionne, vous devez avoir un serveur OSRM en cours d'exécution localement. L'approche recommandée est d'utiliser Docker.

1.  **Installer Docker Desktop**: Si ce n'est pas déjà fait, téléchargez et installez Docker Desktop depuis le site officiel de Docker.
2.  **Télécharger les données OSM pour votre région**: Vous aurez besoin d'un fichier `.osm.pbf` pour la région que vous souhaitez utiliser. Par exemple, pour Berlin:
    ```bash
    wget https://download.geofabrik.de/europe/germany/berlin-latest.osm.pbf
    ```
3.  **Préparer les données OSRM**: Construisez le graphe routier OSRM à partir du fichier PBF:
    ```bash
    docker run -t -v $(pwd):/data osrm/osrm-backend osrm-extract -p /opt/osrm-backend/profiles/car.lua /data/berlin-latest.osm.pbf
    docker run -t -v $(pwd):/data osrm/osrm-backend osrm-partition /data/berlin-latest.osrm
    docker run -t -v $(pwd):/data osrm/osrm-backend osrm-customize /data/berlin-latest.osrm
    ```
4.  **Lancer le serveur OSRM**: Une fois les données préparées, vous pouvez lancer le serveur OSRM:
    ```bash
    docker run -t -i -p 5000:5000 -v $(pwd):/data osrm/osrm-backend osrm-routed --algorithm mld /data/berlin-latest.osrm
    ```
    Le serveur sera accessible à `http://localhost:5000`.

### Exécution du Traitement Cartographique

Pour exécuter le traitement des données cartographiques avec une trace GPS:

```bash
python run_map_processing.py --gpx_file path/to/your/trace.gpx
```

Assurez-vous que le serveur OSRM est en cours d'exécution avant de lancer ce script.

## Dépendances Spécifiques

*   `requests`
*   `gpxpy`
*   `shapely`
*   `folium`
*   `PyQt5`
*   `python-dotenv`

Assurez-vous que ces dépendances sont installées dans votre environnement Python (`pip install -r ../requirements.txt`).


