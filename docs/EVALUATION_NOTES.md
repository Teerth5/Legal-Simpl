# Evaluation notes

Source: the research report in this directory, Results & Analysis. These figures are transcribed from the project report, not rerun by the repository preparation process. The later [exported-notebook review](SUPPLEMENTAL_NOTEBOOK_FINDINGS.md) establishes important protocol limitations and takes precedence over the initial report-only interpretation below.

| Component | Reported result | Scope / limitation |
|---|---|---|
| Retrieval | Hit-rate 0.60; Precision@5 0.80; MRR@5 0.67 | The exported code defines its “precision_at_k” as a binary any-match indicator, not standard Precision@k. Treat as a prototype diagnostic; do not quote 0.80 as standard precision. |
| Risk classifier | Accuracy 0.91; macro-F1 0.8113 | 1,000 synthetic, weak-labelled evaluation clauses; 9,000 train. Not an expert-annotated real-contract benchmark. |
| Risk categories | Yellow F1 0.9283; Red 0.8968; Green 0.6087 | Mean is approximately the reported macro-F1; labels are risk levels, not contract clause types. |
| Domain fine-tuning | F1 approximately 0.33 to 0.56 | Component smoke test discussing 20 categories. This is not a measured threshold-optimization improvement. |
| Boundary trimming | Exact match 0.00 to 0.04 | Separate post-processing experiment; do not attribute to retrieval or risk thresholds. |
| Threshold optimization | Coarse-to-fine search plus evolutionary refinement | Exported notebook includes batch-level before/after examples, but tuning and scoring use the same batches with simulated probabilities. These do not establish held-out improvement. |

Indemnification, liability and force majeure are examples discussed in the report. They do not establish a final production taxonomy or final category-specific risk results.

To reproduce: recover the original application and evaluation code, define document-disjoint train/validation/test splits, record counts and relevance labels, then report retrieval and risk results separately. Fit thresholds on validation data and evaluate once on a held-out test set. Claims of bilingual capability require their own evaluation.
