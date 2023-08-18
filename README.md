# Subgraph KGQA

## LLM Initial Training \& Evaluation

The first part of the repository deals with training a pretrained LLM to obtain our `n` answer candidates for each question of Mintaka. 

To train an LLM from scratch, run the following command:

```python3
python3 tmp.py
```

Alternatively, the beam search outputs from our trained LLM can be found on [HuggingFace](https://huggingface.co/datasets/hle2000/)

## Parsing Wikidata Clone

With our `n` answer candidates, our aim is to extract a subgraph for each <question, answer candidates> pair. In order to do so, we need to parse Wikidata into a local clone using `iGraph`.

To parse the Wikidata Dump, first download a version of choice via [Wikidata](ttps://dumps.wikimedia.org/wikidatawiki/entities/). With the preffered downloaded dump, run the following command:

```python3
python3 tmp2.py
```

## Subgraph Extraction with Wikidata Clone

With our `iGraph` Wikidata clone, we will construct our subgraphs with our `n` answer candidates and `m` question entities (golden entities provided by Mintaka).

To extract subgraphs, run the following command:

```python3
python3 tmp3.py
```

## Subgraphs Reranking

With our subgraphs for each <question, answer candidate> pair, we want to rerank these subgraphs to boost our original `Hits@1` obtained by the original LLM training (first part). We will rerank using the following approaches:

- Deterministic Sequences
- Graphormer

To train the Sequences Ranker from scratch, run the following command:

```python3
python3 tmp4.py
```

To train the Graphormer Ranker from scratch, run the following command:

```python3
python3 tmp5.py
```

To evaluate and rerank the trained ranker model, run the `rerank.ipynb` notebooks within `sequences` and `graphormer` folder respectively.

Alternatively, the trained weights for both approaches can be found on [HuggingFace](https://huggingface.co/datasets/hle2000/). 