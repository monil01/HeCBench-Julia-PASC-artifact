# HeCBench Julia PASC reproducibility artifact

This artifact supports an empirical study of native CUDA, CUDA.jl, KernelAbstractions.jl and JACC.jl. The 447-name assessment contains 436 numerical contracts, two property-only contracts, five execution-only cases and four native hardware barriers. Numerical agreement includes explicitly qualified corrected references and known-defect reproductions; it is not universal scientific validity.

Download the [version 1.0.0 release](https://github.com/monil01/HeCBench-Julia-PASC-artifact/releases/tag/v1.0.0). This separate repository keeps research assets out of the paper's Overleaf checkout.

## Install and replay the supplied analysis

Download `source.tar.gz`, `analysis.tar.gz` and `SHA256SUMS` to an empty directory, then:

```sh
sha256sum -c SHA256SUMS
tar -xzf source.tar.gz
tar -xzf analysis.tar.gz
python3 -m venv analysis-env
analysis-env/bin/pip install -r paper/research/analysis/requirements.txt
analysis-env/bin/python paper/reproduce.py
```

The archives create sibling `source/` and `paper/` trees. The analysis archive also supplies pinned Julia environments and common source headers under `source/`. Python 3.12.3 was used for the author replay. Dependency installation requires network access; the analysis itself uses the provided data. The exact pinned plotting environment is recorded in the requirements file.

The driver recomputes the 447-name census, the 377-name/428-configuration inclusion and native-over-model ratio aggregation, then regenerates family, heat, roofline, implementation-class and timing-control figures. It executes the standalone verification-gate analysis. `paper/research/reproduction_report.json` records scope and elapsed time. Heat error maxima and profile counters are supplied observations: plotting them is not an independent rerun of the original scientific audit.

## Fresh GPU controls

Use a compatible NVIDIA GPU. The recorded system used V100 PCIe 32 GB, driver 580.178.04, Julia 1.12.6, CUDA.jl 6.2.1, KA 0.9.45 and JACC 1.4.0. Native compiler exceptions are explicit; use the exact project/manifests and the control-specific README. Install Julia and CUDA separately, instantiate `source/src/_julia_ka_env` and `source/src/_julia_jacc_env`, and select the GPU deliberately. Never expect identical elapsed times on a different device or host.

- **Timing:** `paper/research/revision_experiments/timing/README.md` documents preparation, `--source-root`, `--julia`, `--nvcc` and `--gpu` options, model order, telemetry and fresh execution. Four counterbalanced blocks each contain five trials; only the first timing in each block is discarded. The saved `compact_results.json` supports CPU analysis with `analyze.py --compact-only --plot`. That mode does not rehash omitted raw GPU arrays.
- **Verification:** `python3 paper/research/revision_experiments/verification/capsule/analyze.py` independently recomputes checks from the supplied small captures. `capsule/run_gpu.py --source-root /absolute/path/to/source --julia /absolute/path/to/julia` produces new candidate executions. Follow the capsule README for GPU selection and subsequent `analyze.py --fresh` use. The incorrect Keccak candidate must be rejected by native/independent gates even though it compiles and passes its shared checker.
- **Fresh translation:** the `translation/` microcontrol contains an immutable native stimulus, evaluation harness, opposite-order arms and every submitted candidate. Its results are a one-workload demonstration, not a statistical order-effect or productivity estimate. Replay requirements and generation/usage scope are recorded alongside the candidates.
- **Ontology:** `classes/README.md` gives the controlled vocabulary, normalization/review procedure, data-only replay and example query. Unknown boundary/size fields remain unknown.

## What is and is not supplied

`source.tar.gz` contains the selected tracked source snapshot at commit `5a6fee7948737c7d0d0c8e4788b690b09f247720`: all 447 native and Julia trees, study tools, ontology records and instructions. The original license and per-directory third-party notices apply. Some large generated inputs excluded from Git have generators/hash records rather than included binary fixtures. Full-corpus execution can require additional runtime assets and is not the same task as the supplied CPU analysis.

The analysis package contains compact scientific records, code, publication files, fresh gate captures and timing telemetry/results. Historical multi-gigabyte GPU captures, local databases and private agent conversations are omitted. Hashes identify omitted captures; they do not make those captures recoverable or prove a new hash audit. Original failed outcomes and corrected-secondary distinctions remain visible. No inference credential is required for analysis or execution; generating new agent translations requires the evaluator's own tool access.

No external artifact badge or independent reproduction is claimed. The measured author setup/replay receipts and limitations are recorded in `ARTIFACT_MANIFEST.json` and the experiment READMEs. Wall times include the explicitly stated setup/lock/JIT scope; dependency download and full-corpus rerun cost are not inferred from short controls.

## Measured author reproduction costs

The complete CPU driver took **25.46 seconds** on the recorded host with dependencies already installed. This includes the figure and table analyses and the compact timing, verification and translation checks; it excludes downloads, installation and LaTeX. The two fresh Keccak processes took **9.042 and 8.891 seconds**, respectively, including lock waiting and Julia startup/JIT. The timing control contains **80 completed processes and 400 trials**, plus one preserved five-trial setup process; recorded per-process telemetry and ordering are supplied. Neither those totals nor the short controls estimate the cost of rerunning all 447 names. A clean extracted-package replay receipt accompanies the release.

The manuscript is a working draft; author metadata and final submission checks remain. The SC-style appendix describes author checks and does not claim an externally awarded badge.
