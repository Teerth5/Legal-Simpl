# Supplemental findings from the exported notebook

The original project has a 929-page PDF export of exploratory notebook code and historical output. It is not an executable source notebook. The raw export is omitted from this public release because it is a lengthy exploratory record rather than runnable source. An initial broad credential-pattern scan produced a false positive from ordinary wording; the corrected token-boundary scan found no matching provider-token patterns. The following focused summary avoids private connection details and redundant logs.

## Risk-classifier experiment (PDF pages 105–125)

- Generated dataset: 10,000 unique synthetic clauses with heuristic/weak labels.
- Stratified split: 9,000 train, 1,000 evaluation.
- Evaluation class counts: GREEN 19, YELLOW 639, RED 342.
- Confusion matrix, rows true / columns predicted in GREEN,YELLOW,RED order: `[[14,5,0],[13,583,43],[0,29,313]]`.
- Accuracy: 910/1,000 = 0.91. Macro-F1 approximately 0.8113; GREEN F1 approximately 0.6087, YELLOW 0.9283, RED 0.8968.
- This is classifier-only evaluation without optimized thresholds. It is not evidence of an RL gain, expert legal-risk correctness or generalization to unseen contract templates. Generated examples from related templates may occur across the split.

## Retrieval diagnostic (PDF pages 19–22)

A sample shuttle-services contract was indexed into 18 chunks. The evaluation code uses tailored questions and regex keyword checks. Its variable named `precision_at_k` is set to 1 if any retrieved chunk matches, rather than counting relevant results and dividing by k. It is therefore an any-match retrieval-hit indicator, not standard precision. Answer-keyword hit rate is a separate quantity. The initial cell also records a missing-registry KeyError; an early code cell does not prove a successful final experiment.

## Threshold experiments (PDF pages 160–183)

Some experiments use handcrafted clauses and simulated Dirichlet probability vectors. The hybrid grid/evolutionary optimizer selects thresholds and scores on the same batches. Reported batch improvements (for example 0.755 to 0.931) are in-sample optimization demonstrations, not held-out model gains. Earlier threshold attempts also degraded scores. No deployment-level improvement is inferred.

## What can responsibly be claimed

The project implements/explores legal-document preprocessing, semantic retrieval, Q&A and risk-classification components. The synthetic classifier experiment is useful evidence of building and evaluating an ML pipeline, provided its data provenance and evaluation scope are explicit. A production legal-risk benchmark requires independently annotated documents, template/document separation, well-defined relevance judgments and untouched test data.
