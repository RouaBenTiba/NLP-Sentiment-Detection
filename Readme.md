# 📝 NLP Sentiment Detection

Application web d'**analyse de texte et de sentiments** développée avec **Python, Streamlit, NLTK, spaCy, TextBlob et OpenAI**.

L'application permet d'explorer un texte à travers plusieurs fonctionnalités : **analyse lexicale, analyse syntaxique et analyse des sentiments**, avec conservation de l'historique des analyses.

---

## 📌 Présentation

Ce projet propose une interface interactive permettant à l'utilisateur de saisir un texte et de réaliser différentes analyses NLP (*Natural Language Processing*).

L'application est organisée autour de trois fonctionnalités principales :

* 🔤 **Analyse lexicale**
* 🌳 **Analyse syntaxique**
* 😊 **Analyse des sentiments**
* 📜 **Historique des analyses**

Une API **Node.js / Express** permet également de communiquer avec **OpenAI** afin d'obtenir une analyse détaillée du texte.

---

## 🎯 Objectifs

Les objectifs du projet sont de :

* comprendre les principales étapes du traitement automatique du langage naturel ;
* effectuer la tokenisation d'un texte ;
* identifier les mots-clés et les stopwords ;
* calculer la fréquence des tokens ;
* analyser la structure syntaxique d'une phrase ;
* identifier le sentiment général d'un texte ;
* comparer plusieurs approches d'analyse des sentiments ;
* intégrer une API d'intelligence artificielle ;
* conserver les résultats des analyses pour les consulter ultérieurement ;
* créer une interface utilisateur interactive avec Streamlit.

---

# 🚀 Fonctionnalités

## 🏠 1. Accueil

La page d'accueil présente l'application et ses principales fonctionnalités.

Elle permet à l'utilisateur de découvrir :

* l'analyse lexicale ;
* l'analyse syntaxique ;
* l'analyse des sentiments.

---

## 🔤 2. Analyse lexicale

L'analyse lexicale permet d'étudier les différents éléments qui composent un texte.

### Tokenisation

Le texte est divisé en différents tokens à l'aide de :

```python
word_tokenize()
```

Exemple :

```text
Bonjour tout le monde !
```

devient :

```text
["Bonjour", "tout", "le", "monde", "!"]
```

### Stopwords

Les mots vides français sont identifiés grâce à NLTK :

```python
stopwords.words("french")
```

L'application distingue alors :

* les mots-clés ;
* les stopwords.

### Fréquence des mots

La fréquence des mots-clés est calculée avec :

```python
FreqDist
```

Les résultats sont ensuite affichés sous forme de tableau avec **Pandas**.

---

# 🌳 3. Analyse syntaxique

L'application utilise **spaCy** avec le modèle français :

```text
fr_core_news_sm
```

Pour chaque token, plusieurs informations sont extraites :

| Information | Description               |
| ----------- | ------------------------- |
| Token       | Mot présent dans le texte |
| Lemma       | Forme de base du mot      |
| POS         | Catégorie grammaticale    |
| Dependency  | Relation syntaxique       |

Exemple de résultat :

```text
Token → Lemma → POS → Dependency
```

L'application génère également un **arbre syntaxique** grâce à :

```python
displacy
```

---

# 😊 4. Analyse des sentiments

L'application utilise plusieurs approches pour analyser les sentiments.

## VADER

L'outil **VADER** fournit un score de sentiment appelé `compound`.

La classification utilisée est :

```text
compound > 0.05    → Positif 😊
compound < -0.05   → Négatif 😞
sinon              → Neutre 😐
```

---

## TextBlob

Le projet utilise également :

```python
TextBlob
```

La polarité du texte permet de déterminer :

```text
polarité > 0 → Positif
polarité < 0 → Négatif
polarité = 0 → Neutre
```

---

## 🤖 Analyse avec OpenAI

Une partie du projet utilise une API Node.js / Express pour communiquer avec OpenAI.

Le fonctionnement est :

```text
Utilisateur
     ↓
Streamlit
     ↓
API Node.js / Express
     ↓
OpenAI
     ↓
Analyse détaillée
     ↓
Streamlit
```

L'application Python envoie le texte à l'API :

```text
POST /api/analyze
```

avec :

```json
{
  "message": "Texte à analyser"
}
```

L'API transmet ensuite le message au modèle OpenAI et retourne le résultat à l'application Streamlit.

---

# 📜 5. Historique

Les résultats des analyses sont enregistrés dans :

```text
results.json
```

Les informations sauvegardées comprennent notamment :

```json
{
    "user_input": "...",
    "vader_sentiment": "...",
    "openai_analysis": "..."
}
```

Les résultats sont organisés par date.

L'utilisateur peut ensuite sélectionner une date dans l'interface afin de consulter les analyses précédentes.

---

# 🏗️ Architecture du projet

L'architecture globale peut être représentée ainsi :

```text
                  ┌──────────────────────┐
                  │      Utilisateur     │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │      Streamlit       │
                  │      Interface       │
                  └──────────┬───────────┘
                             │
             ┌───────────────┼────────────────┐
             │               │                │
             ▼               ▼                ▼
       Analyse          Analyse          Analyse des
       lexicale        syntaxique         sentiments
             │               │                │
             ▼               ▼          ┌─────┴─────┐
           NLTK             spaCy        │           │
                                      VADER      TextBlob
                                             │
                                             ▼
                                       API Node.js
                                             │
                                             ▼
                                           OpenAI
                                             │
                                             ▼
                                        results.json
```

---

# 🛠️ Technologies utilisées

### Frontend / Interface

* **Streamlit**

### NLP

* **NLTK**
* **spaCy**
* **TextBlob**

### Analyse des données

* **Pandas**

### Intelligence artificielle

* **OpenAI API**

### Backend

* **Node.js**
* **Express.js**

### Communication

* **Requests**
* **CORS**

### Stockage

* **JSON**

### Visualisation

* **spaCy displaCy**

### Langages

* **Python**
* **JavaScript**
* **CSS**

---

# 📂 Fonctionnement des différents composants

Le projet contient plusieurs composants correspondant aux différentes fonctionnalités de l'application.

### Application Streamlit

Le fichier principal permet de gérer la navigation entre :

```text
Accueil
Analyse Lexicale & Syntaxique
Analyse des Sentiments
```

La navigation est réalisée avec :

```python
st.sidebar.selectbox()
```

---

### Page d'accueil

La page d'accueil présente les fonctionnalités principales de l'application.

---

### Analyse lexicale et syntaxique

Cette partie utilise :

```text
NLTK
Pandas
spaCy
displaCy
```

pour effectuer les analyses linguistiques.

---

### Analyse des sentiments

Cette partie utilise :

```text
VADER
TextBlob
OpenAI
```

pour produire différentes analyses du texte.

---

### Historique

Les résultats sont sauvegardés dans :

```text
results.json
```

et peuvent être consultés depuis l'application.

---

### API Node.js

Le serveur Express fournit l'endpoint :

```text
POST /api/analyze
```

Il reçoit le texte envoyé par Streamlit et communique avec OpenAI.

---

# 🔄 Pipeline de traitement

Le pipeline principal du projet est :

```text
Saisie du texte
      ↓
Prétraitement / Tokenisation
      ↓
┌───────────────────────────────┐
│                               │
▼                               ▼
Analyse lexicale          Analyse syntaxique
│                               │
├─ Tokens                       ├─ Lemmes
├─ Stopwords                    ├─ POS
├─ Mots-clés                    ├─ Dependencies
└─ Fréquences                   └─ Arbre syntaxique

      ↓

Analyse des sentiments
      ↓
┌───────────┬────────────┐
│           │            │
VADER    TextBlob     OpenAI
│           │            │
└───────────┴────────────┘
             ↓
       Résultats affichés
             ↓
       results.json
```

---

# ⚙️ Installation

## 1. Cloner le projet

```bash
git clone <repository-url>
cd NLP-Sentiment-Detection
```

---

## 2. Créer un environnement virtuel

Windows :

```bash
python -m venv venv
venv\Scripts\activate
```

Linux / macOS :

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## 3. Installer les dépendances Python

```bash
pip install streamlit nltk spacy pandas textblob requests
```

Installer ensuite le modèle français spaCy :

```bash
python -m spacy download fr_core_news_sm
```

---

## 4. Télécharger les ressources NLTK

Le projet utilise notamment :

```python
nltk.download("vader_lexicon")
```

et les ressources nécessaires à la tokenisation et aux stopwords français.

---

# ▶️ Lancer l'application

Lancer l'application Streamlit avec :

```bash
streamlit run app.py
```

Le nom du fichier principal peut être adapté au nom réellement utilisé dans le dépôt.

L'application Streamlit permet ensuite de naviguer entre les différentes fonctionnalités grâce au menu latéral.

---

# 🖥️ Interface

L'application possède une interface permettant de :

* saisir un texte ;
* lancer une analyse lexicale ;
* lancer une analyse syntaxique ;
* analyser les sentiments ;
* consulter l'analyse générée par OpenAI ;
* consulter l'historique des analyses.

Le style graphique est défini dans :

```text
style.css
```

---

# 🔐 Sécurité

Les clés API ne doivent **jamais être directement écrites dans le code source**.

Pour un déploiement réel, il est recommandé d'utiliser une variable d'environnement :

```env
OPENAI_API_KEY=your_api_key
```

Puis côté Node.js :

```javascript
const openai = new OpenAI({
    apiKey: process.env.OPENAI_API_KEY
});
```

Cela évite d'exposer une clé secrète dans un dépôt GitHub public.

---

# 📚 Concepts NLP abordés

Ce projet permet de mettre en pratique plusieurs concepts fondamentaux du NLP :

* Tokenisation
* Stopwords
* Fréquence des mots
* Lemmatization
* Part-of-Speech Tagging
* Dependency Parsing
* Sentiment Analysis
* Lexical Analysis
* Syntax Analysis
* Text Classification

---

# 🎓 Compétences développées

À travers ce projet, les compétences suivantes ont été développées :

### Python

* développement d'applications ;
* manipulation de données ;
* intégration de bibliothèques NLP ;
* gestion de fichiers JSON.

### NLP

* tokenisation ;
* traitement linguistique ;
* analyse lexicale ;
* analyse syntaxique ;
* analyse des sentiments.

### IA

* intégration d'une API LLM ;
* communication avec OpenAI ;
* analyse automatique de texte.

### Web

* création d'une interface interactive avec Streamlit ;
* développement d'une API REST avec Express ;
* communication entre une application Python et un backend Node.js.



# 📌 Résumé

**NLP Sentiment Detection** est une application interactive de traitement automatique du langage naturel permettant d'effectuer :

```text
Analyse lexicale
        +
Analyse syntaxique
        +
Analyse des sentiments
        +
Analyse avec OpenAI
        +
Historique des résultats
```

Le projet combine **Python, NLP, Streamlit et Node.js** afin de proposer une plateforme simple et interactive pour l'exploration et l'analyse de textes.

---

# 👩‍💻 Auteur

**Roua Tiba**

Software Engineering Student | Software Development | DevOps & Cloud

Projet développé dans le cadre de l'apprentissage du **NLP, de l'analyse de texte et de l'intelligence artificielle**.
