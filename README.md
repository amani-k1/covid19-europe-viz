# 🌍 COVID-19 Europe Data Visualization Dashboard  
*Analyse interactive des données COVID-19 en Europe avec Python, MongoDB et Plotly*

---

## 📌 Description du Projet  
Pipeline complet d'analyse des données COVID-19 pour les pays européens :  
1. **Import** des données depuis un fichier CSV  
2. **Stockage** dans une base MongoDB locale  
3. **Nettoyage** et requêtage ciblé (pays européens)  
4. **Visualisation interactive** avec Plotly (graphiques à barres horizontales)  

**Objectif** : Permettre une analyse comparative des décès/confirmés/guérisons entre pays.  

---

## 🛠️ Stack Technique  
### Langages & Bibliothèques  
- **Python 3** (Pandas, PyMongo, Plotly)  
- **MongoDB** (base NoSQL locale)  
- **Visualisation** : Plotly Express (interactivité), Matplotlib/Seaborn  

### Fonctionnalités Clés  
- Filtrage automatique des pays européens  
- Tri par nombre de décès  
- Tooltips interactifs (survol pour voir confirmés/guérisons/actifs)  
- Échelle de couleurs ("Reds") pour l'intensité des décès  

---

## 📊 Visualisation Interactive
![Dashboard COVID-19](images/dashboard.png)
*Graphique des décès par pays européen - Données ECDC*

---

## ⚙️ Structure du Code  
```python
import pandas as pd
from pymongo import MongoClient
import plotly.express as px

# 1. Chargement des données
df = pd.read_csv("country_wise_latest.csv")

# 2. Connexion à MongoDB
client = MongoClient("mongodb://localhost:27017/")
db = client["covid_db"]

# 3. Nettoyage + insertion
collection = db["country_stats"]
collection.delete_many({})
collection.insert_many(df.to_dict("records"))

# 4. Requête Europe
europe_data = collection.find({"WHO Region": "Europe"}, {"_id": 0, ...})

# 5. Visualisation Plotly
fig = px.bar(..., orientation='h', color_continuous_scale="Reds")
fig.show()