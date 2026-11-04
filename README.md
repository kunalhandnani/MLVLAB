# K-Nearest Neighbour (KNN) Virtual Lab

An interactive browser-based virtual laboratory for learning **K-Nearest Neighbour classification**. The application is structured as a Vite project, runs locally, and makes no external API calls. It lets learners move from controlled synthetic examples to real classification datasets in the same interface.

## What learners can do

### 1. Synthetic-data mode

Experiment with three generated 2D classification problems:

- **Two blobs** — a simple two-class problem for first-time KNN exploration.
- **Three classes** — illustrates KNN's natural multi-class behaviour.
- **Two moons** — a curved, non-linear problem that makes decision-boundary behaviour visible.

Change the number of samples, K value, and distance metric. Turn the decision boundary on or off, randomize the layout, and click the plot to place a test point. The lab highlights its K nearest neighbours, draws the distance connections, displays the vote tally, and explains the predicted class.

### 2. Real-dataset mode

Switch to real data and choose two numeric features to create an interactive 2D KNN view. The lab limits visual samples to 300 where necessary so that the decision boundary remains responsive, while retaining the real labels and feature values. Numeric features are z-score standardized before distance calculation so a high-range feature cannot dominate the result.

Bundled datasets are stored in `Datasets/` and are loaded locally by the app:

| Dataset file | Classification target | Available visualization features | Description |
| --- | --- | --- | --- |
| `merged_crop_dataset.csv` | `label` (crop recommendation) | N, P, K, temperature, humidity, pH, rainfall | Crop recommendation observations based on soil nutrients and weather conditions. |
| `Cancer dataset.csv` | `diagnosis` (M / B) | Mean radius, texture, perimeter, area, smoothness, compactness, concavity, concave points | Breast cancer diagnostic measurements. |
| `CAR DETAILS FROM CAR DEKHO.csv` | `fuel` | Year, selling price, kilometres driven | Used-car records, classified by fuel type. |

For readability, real datasets with many possible labels show up to eight classes in the interactive decision-boundary view.

## Learning tools

- **Distance metrics:** Euclidean, Manhattan, and configurable Minkowski distance.
- **Interactive prediction:** click the plot to classify a query point and inspect the closest observations.
- **Evaluation:** deterministic 70/30 holdout split, accuracy, macro precision, macro recall, macro F1 score, confusion matrix, and an accuracy-versus-K chart.
- **Correct preprocessing:** the evaluation description teaches that scaling must be fitted using training data to avoid leakage.
- **Knowledge check:** four-question quiz with explanations.

## KNN workflow shown by the lab

1. Store the labelled training observations.
2. Standardize numeric features when their scales differ.
3. Measure the distance from the query point to every observation.
4. Select the K closest observations.
5. Predict by majority vote. If votes tie, this lab selects the tied class with the smallest total neighbour distance.

Small K values produce detailed, noise-sensitive boundaries; larger K values produce smoother boundaries that can miss local patterns. The decision plot and evaluation chart help learners explore that trade-off.

## Technology

- Vite 7 static web application
- HTML5 Canvas 2D for the decision plots and accuracy chart
- Plain JavaScript and CSS — no charting library, backend, or network service
- CSV datasets bundled with the project

## Getting started

Install dependencies once from the project folder:

```powershell
npm install
```

Start the development server:

```powershell
npm run dev
```

Vite will print a URL such as `http://127.0.0.1:5173/`. Open that exact URL in your browser. Do **not** open `index.html` directly with `file:///...`, because browsers block CSV `fetch()` requests from local files.

Create a production build with:

```powershell
npm run build
npm run preview
```

## Project structure

```text
ML VLAB/
├── index.html                     # Lab interface, styles, and interaction code
├── package.json                   # Vite scripts and dependency
├── README.md
└── Datasets/
    ├── merged_crop_dataset.csv
    ├── Cancer dataset.csv
    └── CAR DETAILS FROM CAR DEKHO.csv
```

## Notes

- The site is fully static. Vite provides the local web server during development, while any static host can serve the production `dist/` folder.
- Evaluation uses the points presently displayed in the selected mode. Its train/test split is deterministic, making changes in K and distance metric easy to compare.
- The browser must be allowed to access the local Vite URL. No internet connection is needed after dependencies are installed.
