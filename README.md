# autoSpectra pre-trained models

Pre-trained soil-property models for the [autoSpectra](https://github.com/HugoMachadoRodrigues/autoSpectra) R package, trained on the Open Soil Spectral Library (OSSL v1.2).

This repository is archived on Zenodo with every release. **Do not download the files by hand:** the package fetches them for you:

```r
library(autoSpectra)
download_ossl_models()          # all four families, one-time setup
predict_soil(my_spectra, "OSSL_VisNIR_Cubist", with_pi = TRUE)
```

## Contents

| File | Family | Algorithm | Properties |
|---|---|---|---|
| `OSSL_VisNIR_Cubist_models.zip` | VisNIR 350–2500 nm | Cubist + PCA(120), replicating Safanelli et al. (2025) | oc, n.tot, ph.h2o, clay.tot |
| `OSSL_MIR_Cubist_models.zip` | MIR 600–4000 cm⁻¹ | Cubist + PCA(120) | oc, n.tot, ph.h2o, clay.tot |
| `OSSL_VisNIR_models.zip` | VisNIR 350–2500 nm | masked soilVAE (accepts partial-coverage instruments) | oc, n.tot, ph.h2o, clay.tot |
| `OSSL_MIR_models.zip` | MIR 600–4000 cm⁻¹ | masked soilVAE | oc, n.tot, ph.h2o, clay.tot |

Each archive holds, per property, the fitted model, the target scaling and calibration range, and a metrics file (held-out metrics, applicability-domain limit, conformal calibration). Since v0.4.1 the metrics files no longer include per-band training ranges. Cubist archives also hold the 10-fold and leave-one-dataset-out cross-validation summaries. `SHA256SUMS` lists the archive checksums.

Performance, methodology and the comparison with Safanelli et al. (2025) are documented in the [autoSpectra README](https://github.com/HugoMachadoRodrigues/autoSpectra#performance).

## No OSSL data is redistributed

These archives contain model parameters and aggregate statistics only. Every archive was checked with `autoSpectra::audit_release_archive()` before publication: no training spectra, lab values, PCA scores of training samples, or per-sample tables. The OSSL itself must be obtained from its [official source](https://docs.soilspectroscopy.org).

## License and citation

The models are derived from OSSL v1.2 (CC BY 4.0) and are released under [CC BY 4.0](LICENSE). If you use them, cite autoSpectra and the OSSL:

- Safanelli JL, Hengl T, Parente LL, Minarik R, Bloom DE, Todd-Brown K, Gholizadeh A, Mendes WdS, Sanderman J (2025). Open Soil Spectral Library (OSSL): Building reproducible soil calibration models through open development and community engagement. *PLOS ONE* 20(1): e0296545. doi:10.1371/journal.pone.0296545
- Safanelli JL, Hengl T, Sanderman J, Parente L (2021). Open Soil Spectral Library (training data and calibration models), v1.2. Zenodo. doi:10.5281/zenodo.7599269
