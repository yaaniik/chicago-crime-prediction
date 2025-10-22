# 🔍 Analisi Predittiva dei Crimini a Chicago

> Modello di Machine Learning per prevedere la probabilità di furti nei quartieri di Chicago utilizzando dati storici


[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Colab](https://img.shields.io/badge/Google-Colab-F9AB00?logo=google-colab)](https://colab.research.google.com/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0+-F7931E?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)

---

## 📋 Panoramica

Questo progetto analizza oltre **7 milioni di crimini** avvenuti a Chicago dal 2001 ad oggi, utilizzando tecniche di Machine Learning per:
- Prevedere la probabilità di furti (THEFT) per quartiere
- Identificare pattern spaziali e temporali
- Supportare le forze dell'ordine nell'allocazione delle risorse

### 🎯 Obiettivo

Stimare la probabilità che si verifichi un furto in ogni quartiere della città utilizzando:
- Dati storici sui crimini
- Informazioni geografiche e temporali
- Algoritmi di classificazione (Random Forest)

---

## 📊 Dataset

### Fonte Dati
**Chicago Data Portal - Crimes (2001 - Present)**  
🔗 Dataset Completo

### Statistiche
- **Record totali**: ~7.000.000+
- **Periodo**: 2001 - Presente
- **Campione analizzato**: 100.000 record (per ottimizzazione performance)
- **Formato**: CSV

### Variabili Principali
| Colonna | Tipo | Descrizione |
|---------|------|-------------|
| `Date` | DateTime | Data e ora del crimine |
| `Primary Type` | Categorical | Tipologia del crimine (THEFT, BATTERY, etc.) |
| `Community Area` | Integer | Codice quartiere (1-77) |
| `Location Description` | Categorical | Descrizione del luogo (STREET, RESIDENCE, etc.) |
| `Latitude/Longitude` | Float | Coordinate geografiche |

---

## 🔬 Metodologia

### 1. Preprocessing

**Operazioni di Pulizia:**
- ✅ Rimozione duplicati
- ✅ Gestione valori mancanti (drop NaN su colonne chiave)
- ✅ Conversione formato data
- ✅ Feature engineering: estrazione Year, Month, Hour

**Feature Selection:**
```python
features = [
    'Community Area',    # Quartiere
    'Location Description',  # Contesto
    'Year', 'Month', 'Hour'  # Dimensione temporale
]
target = 'is_theft'  # 1 se THEFT, 0 altrimenti
```

### 2. Modello Predittivo

**Algoritmo:** Random Forest Classifier

**Motivazione:**
- ✅ Robusto e gestisce dati categoriali/numerici
- ✅ Riduce overfitting
- ✅ Fornisce feature importance
- ✅ Adatto per dataset sbilanciati (con tecniche di bilanciamento)

**Configurazione:**
```python
RandomForestClassifier(
    n_estimators=100,
    max_depth=20,
    random_state=42,
    class_weight='balanced'
)
```

---

## 📈 Risultati

### Metriche di Performance
```
Accuracy:  0.7955
ROC-AUC:   0.7017

Classification Report:
              precision    recall  f1-score   support

           0       0.80      1.00      0.89      7917
           1       0.84      0.02      0.04      2083

    accuracy                           0.80     10000
   macro avg       0.82      0.51      0.46     10000
weighted avg       0.80      0.80      0.71     10000
```

### Insights Chiave

**📍 Distribuzione Geografica:**
- Concentrazione furti nelle zone centrali di Chicago
- Community Area 32 (Loop) mostra il maggior numero di crimini

**📅 Pattern Temporali:**
- Picco crimini: 2003-2004 (~450k/anno)
- Trend decrescente dal 2010
- Calo significativo nel 2020-2021 (COVID-19)

**🕐 Analisi Oraria:**
- Picchi in fasce diurne (10:00-18:00)
- Minimo tra 03:00-05:00

**🏆 Top 3 Tipi di Crimine:**
1. THEFT (~20%)
2. BATTERY (~18%)
3. CRIMINAL DAMAGE (~12%)

---

## 📸 Visualizzazioni

### Mappa di Calore Geografica
<img width="1601" height="783" alt="image" src="https://github.com/user-attachments/assets/b488e807-5d85-4852-81e8-79a35b11abbf" />


### Trend Temporale
<img width="889" height="500" alt="image" src="https://github.com/user-attachments/assets/e4872f8d-2b6f-462d-bca6-9bdd45145e4a" />


### Distribuzione Tipologie
<img width="1296" height="558" alt="image" src="https://github.com/user-attachments/assets/7e629426-4ba7-4bc5-a131-e69cdb312175" />

---

## 🛠️ Tecnologie Utilizzate

**Data Science Stack:**
- `pandas` - Manipolazione dati
- `numpy` - Calcoli numerici
- `scikit-learn` - Machine Learning

**Visualizzazione:**
- `matplotlib` - Grafici statici
- `seaborn` - Visualizzazioni statistiche
- `folium` - Mappe interattive

**Ambiente:**
- `Google Colab`
- Python 3.8+

---

## 📂 Struttura Progetto
```
chicago-crime-analysis/
├── data/
│   └── README.md              # Link al dataset (file troppo grande)
│
├── notebooks/
│   └── README.md              # Link a Google Colab
│
├── reports/
│   ├── Presentazione.pdf      # Slide riassuntiva
│   ├── Report_Completo.pdf    # Analisi dettagliata
│   └── screenshots/           # Immagini visualizzazioni
│
├── docs/
│   └── metodologia.txt        # Note tecniche
│
├── .gitignore
└── README.md                  # Questo file
```

---

## 🚀 Come Usare il Progetto

### Opzione 1: Google Colab (Consigliato)

[![Colab](https://img.shields.io/badge/Google-Colab-F9AB00?logo=google-colab)](https://colab.research.google.com/)

**Accesso diretto al notebook interattivo:**
1. Click sul badge "Open in Colab" sopra
2. Esegui le celle sequenzialmente (Runtime → Run all)
3. Esplora le visualizzazioni e i risultati

### Opzione 2: Esecuzione Locale

**Prerequisiti:**
```bash
python --version  # >= 3.8
```

**Setup:**
```bash
# Clone repository
git clone https://github.com/tuousername/chicago-crime-analysis.git
cd chicago-crime-analysis

# Installa dipendenze
pip install pandas numpy scikit-learn matplotlib seaborn folium jupyter

# Avvia Jupyter
jupyter notebook
```

**Download Dataset:**
1. Vai su Chicago Data Portal
2. Scarica CSV (o usa API per campionamento)
3. Posiziona in `data/crimes.csv`

**Download file ipynb**
1. Vai su Colab Ipynb
2. Scarica il file ipynb colab_chicago_crimes https://drive.google.com/file/d/1Vh1Buixt1XV9j_PueX_UOUlPaXZBfot5/view?usp=drive_link
3. Aprilo con Google Colab

---

## 🔍 Analisi Approfondita

### Sfide Affrontate

**1. Sbilanciamento Classi**
- THEFT rappresenta solo ~20% dei record
- **Soluzione**: `class_weight='balanced'` in Random Forest

**2. Dataset Voluminoso**
- 7M+ record → memoria insufficiente
- **Soluzione**: Campionamento casuale 100k record

**3. Valori Mancanti**
- ~15% record con coordinate mancanti
- **Soluzione**: Drop righe incomplete su feature chiave

### Limitazioni

- ⚠️ **Recall bassa classe "furto"** (0.02): modello conservativo, predice pochi furti
- ⚠️ **Possibili bias**: dati dipendono da segnalazioni effettive (underreporting)
- ⚠️ **Temporalità**: dati pre-2020 potrebbero non riflettere dinamiche post-pandemia

---

## 📊 Metriche Dettagliate

### Confusion Matrix
```
                Predetto
                No THEFT  THEFT
Reale  No THEFT    7891     26
       THEFT        2042     41
```

**Interpretazione:**
- **True Negatives (7891)**: Correttamente identificati non-furti
- **False Positives (26)**: Erroneamente predetti come furti
- **False Negatives (2042)**: Furti non rilevati ⚠️
- **True Positives (41)**: Furti correttamente identificati

### Feature Importance

| Feature | Importanza |
|---------|------------|
| Community Area | 0.42 |
| Hour | 0.28 |
| Location Description | 0.18 |
| Month | 0.08 |
| Year | 0.04 |

---

## 🔮 Sviluppi Futuri

### Miglioramenti Tecnici

- [ ] **SMOTE**: Bilanciamento avanzato delle classi
- [ ] **XGBoost/LightGBM**: Algoritmi gradient boosting
- [ ] **Deep Learning**: LSTM per serie temporali
- [ ] **Feature engineering**: 
  - Distanza da stazioni metro
  - Densità popolazione per quartiere
  - Indicatori economici (reddito medio)

### Applicazioni Pratiche

- [ ] **Dashboard interattiva** (Streamlit/Dash)
- [ ] **API predittiva** per forze dell'ordine
- [ ] **Sistema di alerting** per zone ad alto rischio
- [ ] **Analisi real-time** con dati streaming

---

## 📚 Risorse Aggiuntive

### Documentazione

- 📄 report_chicago_crimes.pdf - Analisi dettagliata
- 🎞️ Exercise_Chicago_Crimes_Presentation.pdf - Slide riassuntiva 9 pagine
- 📝 Esercitazione_Progetto.docx - Traccia

## 👨‍💻 Autore

**Yanik Dimitrov**  
Data Scientist | Machine Learning Engineer

- 🌐 **Portfolio**: yanikdimitrov.vercel.app
- 💼 **LinkedIn**: linkedin.com/in/yanik-dimitrov
- 📧 **Email**: yanik.dimitrov@outlook.com
- 💻 **GitHub**: @yaaniik

---

## 📄 Licenza

Questo progetto è rilasciato sotto licenza **MIT**.

Il dataset è di proprietà della **City of Chicago** ed è rilasciato sotto licenza pubblica.

---

## 🙏 Riconoscimenti

- **City of Chicago** - Per la disponibilità del dataset pubblico
- **Sinergye/Forma.temp Academy AI** - Corso di formazione in Data Science
- **Community Open Source** - Librerie Python utilizzate

---

## 📞 Contatti & Supporto

**Per domande o collaborazioni:**
- 📧 Email: yanik.dimitrov@outlook.com
- 🌟 Lascia una stella se il progetto ti è stato utile!

---

<p align="center">
  <sub>Progetto realizzato per Academy AI - 2025</sub>
</p>
