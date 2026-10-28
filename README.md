# Raman peak extractor for graphene nanoribbon spectra

A browser-based program for baseline subtraction, Si calibration and constrained multi-Lorentzian fitting of Raman spectra of graphene nanoribbons, with uncertainties estimated by a Monte Carlo of the full analysis. It was written for nine-atom-wide armchair graphene nanoribbons (9-AGNRs) on device substrates, and its peak list can be edited for other materials.

<!-- After the Zenodo release: add the DOI badge on the line below this comment, and the reference of the article that used v5. -->

## Running it

The whole program is one file, `index.html`. Download it and open it in a current version of Chrome, Edge, Firefox or Safari; nothing needs to be installed. The page loads the Plotly plotting library and a web font from public servers, so the plots need an internet connection, but the spectra you load are processed inside your browser and are not uploaded anywhere. Settings are remembered in the browser between sessions.

To try the program without your own data, click **Try with simulated example data**. This loads six synthetic spectra generated from the fit values published by Yumigeta et al. (Supporting Information of ref. 1).

## Input

Spectra can be loaded as CSV, TXT, TSV, DAT or ASC files. Spectra stored in columns (first column Raman shift, then one intensity column per spectrum, or alternating shift and intensity columns) and spectra stored in rows (first row Raman shift) are both read, and the layout is detected automatically. Comma, semicolon, tab and whitespace delimiters and decimal commas are recognized, and lines starting with `#`, `//`, `%` or `;` are skipped. For each file you can set a group name (for example as-fabricated and irradiated), the laser power in mW and the integration time in s, which are used to normalize intensities.

## Analysis

Each spectrum is processed in the same sequence: removal of bad CCD pixels and cosmic-ray spikes; calibration of the Raman shift axis to the Si peak (520.5 cm⁻¹ by default); subtraction of a noise-aware adaptive baseline following Lüthi et al. (ref. 2); and Lorentzian fitting of a fixed peak list, with each peak held within a position window and a FWHM range. By default the fit is done region by region (RBLM, Si, CH/D and G), each region with a local linear background and several starting guesses, as in Yumigeta et al. (ref. 1). An adaptive mode that detects peaks automatically and removes weak, nested or limit-bound ones is also available. Two peak models are built in, the default model for transferred 9-AGNRs and the eight-peak model of ref. 1, and peaks can be added, removed or edited.

Uncertainties are reported either from the fit covariance or from a Monte Carlo of the complete pipeline (25 replicas by default), which also captures baseline and peak-overlap uncertainty. Each step is described in the page under **How the analysis works**.

Results can be exported as CSV files (comparison table, peak parameters, ratios and fit quality, group summaries, corrected spectra). **Save methods and settings (MD)** writes a Markdown file with every setting and the program version, intended for the Supporting Information of a paper.

## Validation

The fitting engine was compared with SciPy's `least_squares` on 243 parameters from nine measured spectra and agreed to better than 0.02%.

## How to cite

If you use this program, please cite the version you used:

M. Yusufoglu, Z. Mutlu, Raman peak extractor for graphene nanoribbon spectra (v5), GitHub repository, https://github.com/zmutlulab/raman-peak-extractor (2026).

```bibtex
@misc{RamanPeakExtractor,
  author       = {Yusufoglu, Muhammed and Mutlu, Zafer},
  title        = {Raman peak extractor for graphene nanoribbon spectra (v5)},
  howpublished = {GitHub repository, \url{https://github.com/zmutlulab/raman-peak-extractor}},
  year         = {2026}
}
```

The **Cite this repository** link on the GitHub page gives the same reference, generated from `CITATION.cff`.

<!-- After the Zenodo release: replace the GitHub address in both references above with the DOI of the v5 record. -->

## Methods implemented

1. Yumigeta, K.; Yusufoglu, M.; Federice, J. G.; Hughes, E. T.; Degirmenci, A. M.; Njardarson, J. T.; Simmons-Potter, K.; Potter, B. G.; Mutlu, Z. Electrical and Structural Response of Nine-Atom-Wide Armchair Graphene Nanoribbon Transistors to Gamma Irradiation. *ACS Appl. Mater. Interfaces* **2026**, *18*, 25103–25111. https://doi.org/10.1021/acsami.6c02516
2. Lüthi, D.; Darawish, R.; Müllen, K.; Fasel, R.; Borin Barin, G. Step-Edge Passivation and Quantitative Raman Mapping of Transfer Quality in Aligned Graphene Nanoribbons. arXiv:2606.23304, **2026**. https://arxiv.org/abs/2606.23304

## Development and use of AI

The code was written with the assistance of Claude (Anthropic), a large language model, in 2026. The authors specified the analysis procedure and peak models from the literature above, directed and reviewed the implementation, and validated the fitting results against an independent SciPy fit (see Validation). The authors are responsible for the program and for the results obtained with it.

## License

MIT License. See `LICENSE`.

## Questions and bug reports

Please open an issue in this repository.
