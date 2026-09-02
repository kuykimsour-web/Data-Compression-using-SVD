# SVD Data Compression Using the Wine Dataset

## Project Overview

This project applies **Singular Value Decomposition (SVD)** to the Wine dataset to investigate how a numerical dataset can be represented using a lower-rank approximation while preserving important information.

**Course:** Project II — Data Science and Engineering
**Topic:** Data Compression Using Singular Value Decomposition (SVD)
**Dataset:** Wine Dataset
**Implementation:** Python / Jupyter Notebook

## Objectives

- Load and inspect the Wine dataset.
- Check the dataset for missing values.
- Standardize the numerical features.
- Apply Singular Value Decomposition (SVD).
- Examine the singular values.
- Visualize singular values and their cumulative sum.
- Select a reduced number of components.
- Reconstruct the dataset using a lower-rank SVD approximation.
- Compare the original standardized data with the reconstructed compressed data.

## Dataset

The project uses the Wine dataset available through `sklearn.datasets.load_wine()`.

The dataset contains:

- **178 samples**
- **13 numerical features**
- **3 target classes**

The 13 features are:

1. alcohol
2. malic_acid
3. ash
4. alcalinity_of_ash
5. magnesium
6. total_phenols
7. flavanoids
8. nonflavanoid_phenols
9. proanthocyanins
10. color_intensity
11. hue
12. od280/od315_of_diluted_wines
13. proline

The notebook checks for missing values and finds **0 missing values in every feature**.

## Method

The data is standardized using `StandardScaler` before SVD because the features have different numerical scales. For example, `proline` has substantially larger numerical values than several other features.

SVD decomposes the standardized data matrix as:

X = UΣVᵀ

where:

- `U` contains the left singular vectors.
- `Σ` contains the singular values.
- `Vᵀ` contains the right singular vectors.

The notebook obtains:

- `U`: `(178, 13)`
- `S`: `(13,)`
- `Vᵀ`: `(13, 13)`

## Compression

The notebook selects:

**r = 8**

Only the first eight singular components are retained:

- `U_r = U[:, :8]`
- `S_r = S[:8]`
- `Vᵀ_r = Vᵀ[:8, :]`

The reconstructed matrix is:

X_r = U_r Σ_r Vᵀ_r

The reconstructed dataset keeps the original shape `(178, 13)` but is represented using only eight SVD components instead of thirteen.

## Singular Values

The singular values obtained in the notebook are:

|  r | Singular Value |
| -: | -------------: |
|  1 |      28.942034 |
|  2 |      21.082251 |
|  3 |      16.043716 |
|  4 |      12.789736 |
|  5 |      12.323742 |
|  6 |      10.687140 |
|  7 |       9.903688 |
|  8 |       7.876073 |
|  9 |       7.170818 |
| 10 |       6.682862 |
| 11 |       6.339588 |
| 12 |       5.480976 |
| 13 |       4.289670 |

The first eight components are therefore the components selected for the final reconstruction.

## Visualizations

The notebook includes:

1. **Singular Values vs r** — shows how the singular values change as the number of components increases.
2. **Cumulative Sum of Singular Values vs r** — shows how the cumulative sum changes as additional components are included.

## Results

Before compression, the standardized dataset has shape:

`(178, 13)`

After SVD reconstruction with `r = 8`, the reconstructed dataset also has shape:

`(178, 13)`

The important difference is that the reconstruction is generated from only the first eight singular components.

The notebook also displays the first five rows of both the original standardized data and the reconstructed data for comparison.

## Project Structure

```text
Wine-SVD-Data-Compression/
│
├── Wine dataset Compression.ipynb
├── README.md
├── LICENSE
├── requirements.txt
└── REPORT.pdf
```

## Requirements

Install the required Python packages with:

```bash
pip install -r requirements.txt
```

Then open the notebook using Jupyter Notebook or JupyterLab.

## Reproducibility

The notebook uses the built-in Wine dataset from scikit-learn, so a separate dataset file is not required.

## Conclusion

This project demonstrates how SVD can be used for numerical data compression through a lower-rank approximation. By selecting `r = 8` instead of all 13 singular components, the notebook represents the Wine data using fewer SVD components and reconstructs a matrix with the same original dimensions.

## License

This project is released under the MIT License. See `LICENSE` for details.
