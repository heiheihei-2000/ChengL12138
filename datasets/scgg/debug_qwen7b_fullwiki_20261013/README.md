# Baseline SCGG — HotpotQA FullWiki debug

100 real train questions, 300 pre-retrieval states, 5233220-document BM25 index.
Local Qwen2.5-7B-Instruct BF16, vLLM 0.6.6, NVIDIA RTX A6000.

Training: scgg_dataset.jsonl and scgg_dataset_complete.jsonl (1318 rows).
Offline analysis: labels/labeled_samples.jsonl (1918 rows, including 600 oracle gold-title rows). Do not train on oracle rows.

Labels: local_gain = newly covered gold titles / total gold titles; redundancy = seen retrieved document proportion; answer_gain = sign of HotpotQA EM change; final_gain = local_gain + answer_gain - redundancy (configurable implementation convention).

State evidence comes from earlier real retrievals, but active/backup partition uses gold supporting titles as offline supervision. Post-retrieval docs, answer/correctness metadata and gold annotations must not be used as pre-retrieval predictor inputs. Split by question_id.

Sources and attribution: [HotpotQA](https://hotpotqa.github.io/) ([Yang et al., 2018](https://aclanthology.org/D18-1259/)); [FullWiki train mirror](https://huggingface.co/datasets/hotpotqa/hotpot_qa/tree/main/fullwiki); [official October 2017 Wikipedia abstracts](https://hotpotqa.github.io/wiki-readme.html).
HotpotQA and included Wikipedia text are distributed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). Preserve source attribution. Wiki doc_id and title identify the original article; corpus_source.json records the dump source and checksum.

The 1.55GB corpus archive, full corpus and model weights are not included here. The SCGG rows include the passages needed to inspect each sample. See SCGG_DEBUG_ANALYSIS.md and analysis.json for metrics, 20 random samples and checksums.
