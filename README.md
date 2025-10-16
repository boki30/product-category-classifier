# Product Category Classifier (TF‑IDF + LinearSVC)

Ovaj repozitorijum sadrži Jupyter notebook i uputstvo za treniranje modela koji automatski klasifikuje e‑commerce proizvode na osnovu naslova (kolona "Product Title").

## Šta dobijate
- Notebook za kompletan tok: učitavanje podataka → priprema → treniranje (LinearSVC i ComplementNB) → evaluacija → snimanje artefakata.
- Artefakti evaluacije u `reports/` (classification_report.txt, confusion_matrix.png).
- Snimljen najbolji model u `models/product_category_model.pkl`.

## Struktura repozitorijuma
```
.
├─ data/
│  └─ products.csv                 # vaš dataset (može i sample)
├─ 01_eda_and_modeling.ipynb       # glavni notebook
├─ models/
│  └─ product_category_model.pkl   # snimljen najbolji model (generiše notebook)
├─ reports/
│  ├─ classification_report.txt
│  ├─ confusion_matrix.png
├─ requirements.txt
├─ .gitignore
├─ LICENSE
└─ README.md
```

## Zahtevi
- Python 3.10+
- Paketi iz `requirements.txt` (pandas, numpy, scikit-learn, scipy, matplotlib, seaborn, joblib, jupyter, tqdm)

Instalacija (preporučeno virtualno okruženje):
```bash
python -m venv .venv
# Windows: .venv\Scripts ctivate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
```

## Priprema podataka
- Postavite CSV u `data/products.csv`.
- Minimalno potrebne kolone:
  - `Product Title` (ulazni tekst)
  - `Category Label` (ciljna klasa)
- Ako su nazivi kolona drugačiji, notebook ima automatsko prepoznavanje (case-insensitive, zanemaruje razmake i znake). U slučaju potrebe, ručno ih podesite u konfiguracionoj ćeliji (TEXT_COL, LABEL_COL).

## Pokretanje noteboka (re-trening i generisanje artefakata)
1) Pokrenite Jupyter:
```bash
jupyter notebook
```
2) Otvorite `01_eda_and_modeling.ipynb`.
3) Pokrenite sve ćelije (Kernel → Restart & Run All).
4) Izlazi će biti sačuvani u:
   - `reports/classification_report.txt`
   - `reports/confusion_matrix.png`
   - `models/product_category_model.pkl`

Napomena: Ako broj klasa bude veoma veliki, notebook će automatski ograničiti "punu" konfuzionu matricu na najviše 50 najčešćih klasa da bi graf bio čitljiv i memorijski prihvatljiv.

## Korišćenje modela za inferenciju (van notebook-a)
Primer Python skripte:
```python
import joblib

model = joblib.load("models/product_category_model.pkl")
titles = [
    "apple iphone 8 plus 64gb space grey",
    "dyson v12 cordless vacuum cleaner"
]
preds = model.predict(titles)
for t, p in zip(titles, preds):
    print(f"{t} -> {p}")
```

## Reproduktivnost
- Fiksiran `random_state=42` gde je primenljivo.
- Verzije paketa su u `requirements.txt`.
- Notebook snima sve artefakte kako bi se evaluacija mogla proveriti.

## Saveti
- Ako je `models/product_category_model.pkl` > 100MB, koristite Git LFS (`git lfs install` i `git lfs track "*.pkl"`).
- Ako ne delite ceo dataset, dodajte `data/sample_products.csv` i kratak `data/README.md` sa uputstvom kako pribaviti puni skup.

## Licenca
MIT (vidi LICENSE)
