# 🔍 Analisi Predittiva dei Crimini a Chicago

> Modello di Machine Learning per prevedere la probabilità di furti nei quartieri di Chicago utilizzando dati storici

[![Python](https://img.shields.io/badge/Python-3.10-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Colab](https://img.shields.io/badge/Google-Colab-F9AB00?logo=google-colab)](https://colab.research.google.com/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.2+-F7931E?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)

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
🔗 [Dataset Completo](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2/about_data)

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
    'Community Area',        # Quartiere
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
<img width="1601" height="783" alt="Heatmap crimini Chicago" src="https://github.com/user-attachments/assets/b488e807-5d85-4852-81e8-79a35b11abbf" />

*Distribuzione geografica dei crimini con concentrazione nelle zone centrali*

---

### Trend Temporale
<img width="889" height="500" alt="Trend annuale crimini" src="https://github.com/user-attachments/assets/e4872f8d-2b6f-462d-bca6-9bdd45145e4a" />

*Evoluzione del numero di crimini dal 2001 al 2025*

---

### Distribuzione Tipologie
<img width="1296" height="558" alt="Distribuzione crimini per tipologia" src="https://github.com/user-attachments/assets/7e629426-4ba7-4bc5-a131-e69cdb312175" />

*Top tipologie di crimine più frequenti*

---

## 🛠️ Tecnologie Utilizzate

**Ambiente di Sviluppo:**
- **Google Colab** - Notebook cloud con GPU gratuita
- **Google Drive** - Storage dataset

**Data Science Stack:**
- `pandas 1.5+` - Manipolazione dati
- `numpy 1.23+` - Calcoli numerici
- `scikit-learn 1.2+` - Machine Learning

**Visualizzazione:**
- `matplotlib 3.7+` - Grafici statici
- `seaborn 0.12+` - Visualizzazioni statistiche
- `folium 0.14+` - Mappe interattive

**Versione Python:** 3.10 (Google Colab runtime)

---

## 📂 Struttura Progetto
```
chicago-crime-prediction/
├── data/
│   └── README.md              # Link al dataset
│
├── notebooks/
│   └── README.md              # Link a Google Colab
│
├── reports/
│   ├── Exercise_Chicago_Crimes_Presentation.pdf  # Slide (9 pagine)
│   ├── report_chicago_crimes.pdf                 # Report completo            
├── docs/
│   └── Esercitazione_Progetto.docx # Traccia
│
├── .gitignore
└── README.md                  # Questo file
```

**Nota:** Il notebook (`.ipynb`) è ospitato su Google Colab e non è incluso nel repository.

---

## 🚀 Come Usare il Progetto

### Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Vh1Buixt1XV9j_PueX_UOUlPaXZBfot5)

**Accesso diretto al notebook:**

1. Click sul badge "Open in Colab" sopra
2. Il notebook si aprirà automaticamente in Google Colab
3. **(Opzionale)** Salva una copia: **File → Save a copy in Drive**
4. Esegui tutte le celle: **Runtime → Run all**
5. Attendi il completamento (~10-15 minuti)
6. Esplora visualizzazioni e risultati

**Requisiti:**
- ✅ Account Google (gratuito)
- ✅ Browser web
- ❌ Nessuna installazione locale necessaria
- ❌ Nessun setup Python richiesto

**Note:**
- Il notebook carica automaticamente i dati da URL pubblico
- Esecuzione nel cloud di Google (GPU disponibile gratuitamente)
- Modifiche salvate automaticamente su Drive (se salvi copia)

**Link alternativi:**
- 📂 [Visualizza su Drive](https://drive.google.com/file/d/1Vh1Buixt1XV9j_PueX_UOUlPaXZBfot5/view?usp=drive_link) (solo lettura)
- ⬇️ [Download .ipynb](https://drive.google.com/uc?export=download&id=1Vh1Buixt1XV9j_PueX_UOUlPaXZBfot5) (backup locale)

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

---

### Limitazioni

- ⚠️ **Recall bassa classe "furto"** (0.02): modello conservativo
- ⚠️ **Possibili bias**: dipendenza da segnalazioni effettive
- ⚠️ **Temporalità**: dinamiche pre-2020 potrebbero differire dal post-pandemia

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
- **True Negatives (7891)**: Correttamente identificati come non-furti ✅
- **False Positives (26)**: Erroneamente predetti come furti
- **False Negatives (2042)**: Furti non rilevati ⚠️
- **True Positives (41)**: Furti correttamente identificati ✅

---

### Feature Importance

| Feature | Importanza | Impatto |
|---------|------------|---------|
| Community Area | 0.42 | 🔴 Molto Alto |
| Hour | 0.28 | 🟠 Alto |
| Location Description | 0.18 | 🟡 Medio |
| Month | 0.08 | 🟢 Basso |
| Year | 0.04 | 🟢 Basso |

---

## 🔮 Sviluppi Futuri

### Miglioramenti Tecnici

- [ ] **SMOTE**: Bilanciamento avanzato delle classi
- [ ] **XGBoost/LightGBM**: Algoritmi gradient boosting
- [ ] **Deep Learning**: LSTM per serie temporali
- [ ] **Feature Engineering**: 
  - Distanza da stazioni metro
  - Densità popolazione per quartiere
  - Indicatori economici (reddito medio)

### Applicazioni Pratiche

- [ ] **Dashboard interattiva** (Streamlit/Dash)
- [ ] **API predittiva** per forze dell'ordine
- [ ] **Sistema di alerting** automatico
- [ ] **Analisi real-time** con dati streaming

---

## 📚 Risorse Aggiuntive

### Documentazione

- 📄 [Report Completo](reports/report_chicago_crimes.pdf) - Analisi dettagliata
- 🎞️ [Presentazione](reports/Exercise_Chicago_Crimes_Presentation.pdf) - Slide (9 pagine)
- 📋 [Traccia Progetto](reports/Esercitazione_Progetto.docx) - Requisiti originali

### Link Utili

- 🔗 [Chicago Data Portal](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2/about_data)
- 📊 [Scikit-learn Docs](https://scikit-learn.org/stable/documentation.html)
- 🗺️ [Folium Tutorial](https://python-visualization.github.io/folium/)

---

## 👨‍💻 Autore

**Yanik Dimitrov**  
Data Scientist | Machine Learning Engineer

- 🌐 **Portfolio**: [yanikdimitrov.vercel.app](https://yanikdimitrov.vercel.app/)
- 💼 **LinkedIn**: [linkedin.com/in/yanik-dimitrov](https://www.linkedin.com/in/yanik-dimitrov/)
- 📧 **Email**: yanik.dimitrov@outlook.com
- 💻 **GitHub**: [@yaaniik](https://github.com/yaaniik)

---

## 📄 Licenza

Il dataset è di proprietà della **City of Chicago** ed è rilasciato sotto licenza pubblica.

---

## 🙏 Riconoscimenti

**Organizzazioni:**
- **City of Chicago** - Per il dataset pubblico
- **Sinergye/Forma.temp Academy AI** - Formazione in Data Science

**Tecnologie:**
- **Google** - Per Colab e infrastruttura cloud
- **Python Community** - Per le librerie open source

---

## 📞 Contatti & Supporto

**Per domande o collaborazioni:**

- 📧 **Email**: yanik.dimitrov@outlook.com
- 🌟 **Lascia una stella** se il progetto ti è stato utile!

---

<p align="center">
  <sub>Progetto realizzato per Sinergye/Forma.temp Academy AI - 2025</sub>
</p>
