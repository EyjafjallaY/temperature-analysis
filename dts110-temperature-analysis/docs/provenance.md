# Data and code sources

## External resources

The temperature dataset and the `Climate` and `se_over_slope` helper implementations correspond to **MIT OpenCourseWare, 6.0002 Introduction to Computational Thinking and Data Science, Fall 2016, Problem Set 5: Modeling Global Warming**, by Eric Grimson, John Guttag and Ana Bell.

- [Official resource page](https://ocw.mit.edu/courses/6-0002-introduction-to-computational-thinking-and-data-science-fall-2016/resources/ps5/)
- [Official archive](https://ocw.mit.edu/courses/6-0002-introduction-to-computational-thinking-and-data-science-fall-2016/f5682c4bfaad90428a6e9fd82c66b27a_PS5.zip)
- [MIT OCW terms](https://ocw.mit.edu/pages/privacy-and-terms-of-use/)
- [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

Copyright in the upstream OCW materials remains with Massachusetts Institute of Technology and the respective rights holders. Institutional names identify the external sources and do not indicate endorsement.

Verification on 2026-10-08 established that the CSV matches the official archive byte-for-byte. The executable AST bodies of `Climate` and `se_over_slope` match the upstream `ps5.py` after excluding docstrings and source positions.

## Analysis implementation

`Climate` supplies CSV loading and temperature lookup. `se_over_slope` supplies the statistical diagnostic used for linear fits. The following project functions implement regression, aggregation, smoothing, evaluation and variability analysis:

| Function | Role |
| --- | --- |
| generate_models | Fit requested polynomial degrees |
| r_squared | Calculate training goodness of fit |
| evaluate_models_on_training | Plot training fits and diagnostics |
| gen_cities_avg | Aggregate city annual means |
| moving_average | Compute trailing-window means |
| rmse | Calculate prediction error |
| evaluate_models_on_testing | Plot held-out comparisons |
| gen_std_devs | Compute within-year variability of daily cohort means |

The analysis includes model comparisons, result visualizations and interpretation. Possible industrial applications are discussed in [analysis notes](analysis.md#possible-applications); implementing them would require additional data and models.

## Reproduction record

The complete notebook was run using a new kernel in an existing environment: Python 3.11.14, NumPy 2.4.2, Matplotlib 3.10.8, nbclient 0.10.2, nbformat 5.10.4, ipykernel 6.29.5 and jupyter_client 8.6.3. All 22 code cells completed and all six assertion groups passed. Four-decimal results matched the stored figures and reported metrics; the high-degree conditioning warning was retained.

The notebook outputs and ten PNG figures present the experimental results. The dataset is unchanged from the referenced archive. Reproduction was checked through a temporary execution copy; a fresh dependency installation was not tested.

## License scope

The upstream resources use CC BY-NC-SA 4.0. This project and its documentation are distributed under the same license, preserving the attribution, noncommercial and share-alike terms. See [LICENSE](../LICENSE). Third-party Python dependencies retain their own licenses and are not bundled.

The noncommercial restriction applies to reuse. Public source visibility does not grant unrestricted commercial use or permission to relicense upstream materials.
