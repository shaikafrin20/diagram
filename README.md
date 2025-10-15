## 🧱 System Architecture — Loan Default Risk Prediction

```mermaid
<-- paste code here -->
flowchart TD
  subgraph Data[Data & Storage]
    A1[Loan_default.csv (Raw dataset)]
    A2[Preprocessed data (features engineered)]
    A3[Trained model file (model.pkl / joblib)]
  end

  subgraph ModelPipeline[Model Training Pipeline]
    B1[Notebook: loan.ipynb]
    B2[Preprocessing & Feature Engineering]
    B3[Model Training & Evaluation]
    B4[Save model artifact]
  end

  subgraph Backend[Flask Backend]
    C1[app.py (Flask routes)]
    C2[/predict endpoint]
    C3[/get_statistics endpoint]
    C4[Model loader (load model.pkl)]
    C5[Data processing utils (pandas, sklearn)]
  end

  subgraph Frontend[Web UI]
    D1[Landing page: /]
    D2[Dashboard: /dashboard]
    D3[Input form (16 features)]
    D4[Visualizations (matplotlib / seaborn)]
  end

  subgraph Static[Static & Templates]
    E1[templates/*.html]
    E2[static/css (Tailwind)]
    E3[static/js (vanilla JS)]
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

  %% Notes for clarity
  %% Use simple text nodes; GitHub Mermaid doesn't support multiline
  %% To render: paste in VS Code (with Mermaid extension) or mermaid.live
