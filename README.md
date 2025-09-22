# Tydzień 8 — NLP: wektoryzacja, sentyment, klasyfikacja, tematy

Podsumowanie tygodnia pracy nad NLP: od przygotowania tekstu, przez wektoryzację (CountVectorizer/TF‑IDF), po modele ML (NB/LR) i modelowanie tematów (NMF). Dołączam krótki opis, jak uruchomić notatniki oraz najciekawsze wnioski.

## TL;DR
- Wejście w wektoryzację tekstu: DTM (CountVectorizer) i TF‑IDF.
- Sentyment (VADER) + wskazówki dla języka polskiego (własny leksykon).
- Klasyfikacja tekstu: Naive Bayes i Logistic Regression na recenzjach.
- Modelowanie tematów: NMF na macierzy TF‑IDF — przegląd wiodących tematów.

## Co jest w repo
- `section3_nlp_basics/src/3_vectorization.ipynb` — praktyka: CountVectorizer, TF‑IDF, n‑gramy, częstotliwości terminów, wykresy.
- `section4_nlp_machine_learning/section4_nlp_with_machine_learning_code.ipynb` — sentyment, klasyfikacja (NB/LR), modelowanie tematów (NMF) i łączenie technik.
- `section4_nlp_machine_learning/section4_assignments.ipynb` — zadania do samodzielnego przerobienia.
- `Data/` — pliki danych wykorzystywane w notatnikach (CSV/XLSX).

Uwaga: jeśli pracujesz po polsku z VADER, przygotuj własny leksykon (np. `Data/vader_lexicon_pl.txt`) i podaj go do konstruktora `SentimentIntensityAnalyzer(lexicon_file=...)`.

## Jak uruchomić (Windows/PowerShell)
1) Aktywuj środowisko (użyj tego, którego używasz do notatników):
```powershell
# przykładowo
.\nlp_machine_learning\Scripts\Activate.ps1
```
2) Zainstaluj zależności:
```powershell
pip install -r requirements.txt
```
3) Uruchom Jupyter i otwórz notatniki:
```powershell
jupyter notebook
```
- Otwórz: `section3_nlp_basics/src/3_vectorization.ipynb`
- Otwórz: `section4_nlp_machine_learning/section4_nlp_with_machine_learning_code.ipynb`

## Najważniejsze elementy techniczne
- Wektoryzacja:
  - `CountVectorizer` (słowa i n‑gramy) oraz `TfidfVectorizer` (wagi TF‑IDF).
  - Parametry: `stop_words`, `ngram_range`, `min_df`/`max_df` — kontrolują jakość i rozmiar słownika.
- Sentyment:
  - VADER — szybki baseline dla EN; dla PL → własny leksykon i ostrożność z negacją („nie”).
  - Funkcja `get_sentiment` zwraca wynik `compound` w [−1, 1].
- Klasyfikacja:
  - Porównanie Naive Bayes vs Logistic Regression na wektorach Bag‑of‑Words/TF‑IDF.
  - Metryki: `accuracy`, `classification_report` (precision/recall/F1 per klasa).
- Tematy (NMF):
  - TF‑IDF → NMF (`n_components`) → top słowa na temat i przypisanie dokumentów do tematów.

## Wyniki i obserwacje
- TF‑IDF zwykle daje lepsze wyniki niż czyste zliczenia, zwłaszcza przy bigramach.
- Logistic Regression często wygrywa z Naive Bayes dla zbalansowanych, krótkich tekstów.
- NMF pozwala szybko „zobaczyć” główne wątki w zbiorze — dobre do eksploracji przed ML.

## Następne kroki (plan)
- Dodać polski leksykon VADER i przetestować na większym zbiorze PL.
- Spróbować embeddingów zdań (`sentence-transformers`) i lekkiego klasyfikatora (LR/SVM).
- Fine‑tuning modelu PL (np. `herbert-base`, `polish-roberta`) pod klasyfikację nagłówków/recenzji.

## Kontakt
Jeśli chcesz dopytać lub podyskutować: LinkedIn — podsumowanie Tygodnia 8 i wnioski z nauki NLP.
