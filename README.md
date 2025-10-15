# diagram
# Block Diagram — Loan Default Risk Prediction

Below is a clear block diagram (Mermaid) that matches the project structure from your uploaded files (README.md and loan.ipynb). It shows data flow from dataset → preprocessing → model training → model artifact → Flask backend → Frontend UI and Dashboard, plus auxiliary components (visualizations, APIs, static assets).

```mermaid
flowchart TD
  subgraph Data[Data & Storage]
    A1[Loan_default.csv\n(Raw dataset)]
    A2[Preprocessed data\n(features engineered)]
    A3[Trained model file\n(model.pkl / model.joblib)]
  end

  subgraph ModelPipeline[Model Training Pipeline]
    B1[Notebook: loan.ipynb]
    B2[Preprocessing & Feature Eng]
    B3[Model Training & Eval]\n    B4[Save model artifact]
  end

  subgraph Backend[Flask Backend]
    C1[app.py\n(Flask routes)]
    C2[/predict endpoint]\n    C3[/get_statistics endpoint]\n    C4[model loader\n(load model.pkl)]
    C5[Data processing utils\n(pandas, sklearn)]
  end

  subgraph Frontend[Web UI]
    D1[Landing page: /]\n    D2[Dashboard: /dashboard]\n    D3[Input form (16 features)]
    D4[Visualizations\n(matplotlib/seaborn static images)]
  end

  subgraph Static[Static & Templates]
    E1[templates/*.html]\n    E2[static/css (Tailwind)]\n    E3[static/js (vanilla JS)]
  end

  A1 --> B2
  B2 --> B3
  B3 --> B4
  B4 --> A3

  A3 --> C4
  C4 --> C1
  C1 --> C2
  C1 --> C3
  C2 -->|POST JSON| D3
  D3 -->|AJAX| C2
  C3 -->|GET| D4

  E1 --> D1
  E1 --> D2
  E2 --> D1
  E3 --> D2

  B1 --> B2
  B1 --> B3

  classDef data fill:#f9f,stroke:#333,stroke-width:1px;
  class A1,A2,A3 data;

  note right of C1
    Key libs: Flask, scikit-learn,
    pandas, matplotlib, seaborn
  end

  note left of D3
    Inputs: Age, Income,\nCreditScore, LoanAmount,\nInterestRate, DTIRatio, etc.
  end
```

---

## Short explanations (visible in canvas)

* **Data & Storage**: Your raw CSV (`Loan_default.csv`) is preprocessed (cleaning, encoding, scaling). The notebook (`loan.ipynb`) performs EDA, preprocessing, model training and evaluation, then saves the final model artifact (`model.pkl` or `model.joblib`).

* **Model Training Pipeline**: Steps performed inside `loan.ipynb` — feature engineering, model training (e.g., logistic regression / tree / ensemble), evaluation (confusion matrix, ROC), and model serialization.

* **Backend (Flask)**: `app.py` exposes endpoints:

  * `GET /` — landing page
  * `GET /dashboard` — dashboard view with statistics and visualizations
  * `POST /predict` — accepts applicant JSON, runs preprocessing, loads model, returns default probability
  * `GET /get_statistics` — returns aggregated metrics and plots

* **Frontend**: HTML + Tailwind and vanilla JS provide the form for inputting the 16 features, call `/predict` via AJAX, and render the returned prediction and visualizations.

* **Static & Templates**: Typical Flask structure with `templates/` for Jinja HTML and `static/` for Tailwind CSS and JavaScript.

---

If you'd like, I can:

* Export this diagram as a PNG or SVG for use in your README or presentation.
* Produce a simplified one-page slide PNG with the diagram and a short caption.

Tell me which format you want (PNG, SVG, or PDF) and I'll export it directly into the canvas as a downloadable file.
