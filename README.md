# KWELA

**Kinetic Weighted Evaluation for Latent Amyloid**

Specialized RT-QuIC classification for complex environmental matrices.

## Overview

KWELA extends RT-QuIC (Real-Time Quaking-Induced Conversion) statistical analysis to complex environmental matrices through matrix-specific calibration. It provides the statistical framework needed to reliably apply RT-QuIC in environmental surveillance contexts where standard statistical approaches may be confounded by matrix-induced artifacts.

KWELA is a **specialized complement** to standard statistical methods (ANOVA, t-tests, AUC), not a replacement. Standard methods work well for laboratory conditions with clean samples. KWELA addresses the gap when environmental matrix complexity introduces artifacts that confound interpretation.

## Status

**CRAN submission pending.** Package source will be available here upon acceptance.

## Features

- **Robust Classification**: Positive-control-anchored Z-score transformations with logistic calibration and kinetic shape gating
- **Auto-Detection**: Automatically detects RT-QuIC vs Nano-QuIC and applies optimized thresholds
- **Interference Detection**: Continuous interference score based on metric correlation dissociation
- **Concordance Analysis**: Per-treatment CCC/RMSE/MBE against positive control profiles
- **Predictive Projection**: Projects classification reliability based on metric-space distance from positive controls
- **Classification Entropy**: Measures boundary quality per treatment group
- **Robust Statistics**: Adaptive scale estimation (MAD, Sn, Qn) with Rousseeuw-Croux (1993) finite-sample corrections
- **Plugin Architecture**: Accepts standard data frames from any upstream source (e.g., [quicR](https://github.com/gage1145/quicR))

## Installation

```r
# Available after CRAN acceptance:
# install.packages("KWELA")
```

## Quick Start

```r
library(KWELA)

# Run the built-in demo
demo_kwela()

# Analyze your data
result <- kwela("my_rtquic_data.csv")

# With full evaluation (interference, concordance, projection)
result <- kwela(my_dataframe, evaluate = TRUE)
eval_report <- attr(result, "evaluation")
```

## When to Use KWELA vs Standard Methods

| Approach | Best For |
|----------|----------|
| **Standard methods** (ANOVA, t-tests, AUC) | Laboratory conditions, clean samples, well-characterized matrices |
| **KWELA** | Environmental matrices with unknown interference, complex multi-component samples, QC assessment |

## Plugin Compatibility

KWELA accepts standard data frames with columns: `Treatment`, `TTT`, `MS`, `MP`, `RAF`. Any upstream package can produce these — use `kwela_validate()` to check compatibility.

```r
# Example: quicR -> KWELA pipeline
metrics <- quicR::calculate_metrics(raw_data, meta)
kwela_validate(metrics)
result <- kwela(metrics, evaluate = TRUE)
```

## Author

Richard A. Feiss IV, Ph.D.  
Minnesota Center for Prion Research and Outreach (MNPRO)  
University of Minnesota

## License

MIT
