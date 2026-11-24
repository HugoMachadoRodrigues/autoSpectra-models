# autoSpectra pre-trained models

Pre-trained soil-property models for the [autoSpectra](https://github.com/HugoMachadoRodrigues/autoSpectra) R package, trained on the Open Soil Spectral Library (OSSL v1.2).

This repository is archived on Zenodo with every release. **Do not download the files by hand:** the package fetches them for you:

```r
library(autoSpectra)
download_ossl_models()          # default: VisNIR/MIR PCA-VAE and Cubist
download_ossl_models("all")     # every family below
predict_soil(my_spectra, "OSSL_VisNIR_PCAVAE", with_pi = TRUE)
predict_soil_agnostic(my_spectra, "visnir")   # any instrument range
```

## Contents

Each family is one `<family>_models.zip`, or several `<family>_models.part<k>.zip` when it would pass GitHub's 100 MB file limit (the package reassembles them).

| Family | Spectra | Algorithm | Properties |
|---|---|---|---|
| `OSSL_VisNIR_Cubist` | VisNIR 400–2500 nm | Cubist + PCA(120), replicating Safanelli et al. (2025) | 23 |
| `OSSL_MIR_Cubist` | MIR 600–4000 cm⁻¹ | Cubist + PCA(120) | 42 |
| `OSSL_NeoSpectra_Cubist` | NeoSpectra 1350–2550 nm | Cubist + PCA(120) | 29 |
| `OSSL_VisNIR_PCAVAE` | VisNIR 400–2500 nm | ensemble of 5 soilVAE on the same 120 PCs | 23 |
| `OSSL_MIR_PCAVAE` | MIR 600–4000 cm⁻¹ | same | 42 |
| `OSSL_NeoSpectra_PCAVAE` | NeoSpectra 1350–2550 nm | same | 29 |
| `OSSL_VisNIR_PCAVAE_800` / `_1000` / `_1350` | VisNIR from 800, 1000 or 1350 to 2500 nm | PCA-VAE on one instrument window | 23 |
| `OSSL_MIR_PCAVAE_700_3800` | MIR 700–3800 cm⁻¹ | PCA-VAE on one instrument window | 42 |
| `KSSL_VisNIR_Cubist`, `KSSL_MIR_Cubist`, `KSSL_VisNIR_PCAVAE`, `KSSL_MIR_PCAVAE` | as OSSL | the OSSL pipeline trained on the KSSL rows only | 6 / 41 |

`predict_soil_agnostic()` sends each spectrum to the PCA-VAE of the widest window it covers, so instruments covering only part of the range are predicted too. The masked soilVAE families (`OSSL_VisNIR`, `OSSL_MIR`) of v0.4.x are no longer published: the window models are clearly more accurate (mean R² 0.735 vs 0.578 VisNIR, 0.802 vs 0.666 MIR).

Each archive holds, per property, the fitted model (Cubist bundle or the 5 soilVAE weights plus the PCA loadings), the target scaling, and a metrics file (held-out metrics, applicability-domain limits for the Q-statistic and, from v0.5.1, Hotelling T2, conformal calibration), plus a family-level `metrics_summary.json`. `SHA256SUMS` lists the archive checksums.

Performance, methodology and the comparison with Safanelli et al. (2025) are documented in the [autoSpectra README](https://github.com/HugoMachadoRodrigues/autoSpectra#performance).

## No OSSL data is redistributed

These archives contain model parameters and aggregate statistics only. Every archive was checked with `autoSpectra::audit_release_archive()` before publication: no training spectra, lab values, PCA scores of training samples, embedded Cubist training matrices (`$data`, or `$train` in Cubist >= 1.0), or per-sample tables. The OSSL itself must be obtained from its [official source](https://docs.soilspectroscopy.org).

## License and citation

The models are derived from OSSL v1.2 (CC BY 4.0) and are released under [CC BY 4.0](LICENSE). If you use them, cite autoSpectra and the OSSL:

- Safanelli JL, Hengl T, Parente LL, Minarik R, Bloom DE, Todd-Brown K, Gholizadeh A, Mendes WdS, Sanderman J (2025). Open Soil Spectral Library (OSSL): Building reproducible soil calibration models through open development and community engagement. *PLOS ONE* 20(1): e0296545. doi:10.1371/journal.pone.0296545
- Safanelli JL, Hengl T, Sanderman J, Parente L (2021). Open Soil Spectral Library (training data and calibration models), v1.2. Zenodo. doi:10.5281/zenodo.7599269
