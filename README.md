```mermaid
flowchart TD
    %% Source Datasets
    A[Source Datasets<br/><small>CMAPSS: 21k cycles<br/>AI4I: 10k instances</small>] 

    %% Preprocessing
    B[Preprocessing<br/><small>Z-score, Window=30</small>]

    %% Source Embeddings
    C[Source Embeddings<br/><small>Transformer</small>]

    %% Nigerian Perturbations
    D[Nigerian Perturbations<br/><small>Humidity 80% Drift<br/>Sabotage Spikes<br/>Power Dropout 30%</small>]

    %% Target Synthesis
    E[Target Synthesis<br/><small>SDV GaussianCopula</small>]

    %% Target Embeddings
    F[Target Embeddings<br/><small>w/ Nigerian Noise</small>]

    %% Gradient Reversal Layer
    G[Gradient Reversal Layer<br/><small>GRL λ=0.1</small>]

    %% Domain Discriminator
    H[Domain Discriminator]

    %% RUL Predictor
    I[RUL Predictor<br/><small>XGBoost + Weibull</small>]

    %% SimCLR Self-Supervised
    J[SimCLR Self-Supervised<br/><small>Alignment (70% Unlabeled)</small>]

    %% Multifaceted Outputs
    K[Multifaceted Outputs<br/><small>• AUPRC (Imbalanced Failures)<br/>• RMSE/MAE (RUL Cycles)<br/>• TCO (Monte Carlo, $10M/day Downtime)</small>]

    %% Deployment
    L[Deployment Protocols<br/><small>FastAPI + Docker</small>]

    %% Connections
    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
    F --> G
    G --> H
    G --> I
    C --> J
    F --> J
    J --> K
    K --> L

    %% Styling
    classDef dataset fill:#E8F5E9,stroke:#4CAF50,stroke-width:2px,color:#1B5E20
    classDef process fill:#E3F2FD,stroke:#1976D2,stroke-width:2px,color:#0D47A1
    classDef model fill:#FFF3E0,stroke:#F57C00,stroke-width:2px,color:#E65100
    classDef output fill:#F3E5F5,stroke:#7B1FA2,stroke-width:2px,color:#4A148C
    classDef deploy fill:#E0F2F1,stroke:#00695C,stroke-width:2px,color:#004D40

    class A dataset
    class B,D,E process
    class C,F,G model
    class H,I,J model
    class K output
    class L deploy
```
