# MultiGrid-Transformer
Prototype implementation of grid of tokens representation for Transformers

## 🔍 Summary
- Leverages auxiliary token axes (e.g., frames, roles, abstractions)
- Early tests on synthetic data show improved token prediction accuracy
- Seeks collaboration to apply to real-world benchmarks

## Motivation
Transformer base model has to learn and to re-learn many things from scratch. Some of these studies are c

## How It Works

This research proposes to enrich Transformer’s input, interim and output representations from the _unidirectional sequence of tokens_ to the _grid of tokens_ (see the illustration below).
The original sequence of tokens gets accompanied with parallel meta sequences of meta tokens, each containing additional information. It implies changes to the Transformer’s operations:

- Instead of a one-dimensional stream of tokens processed left-to-right, the model would process a multi-dimensional grid:
  - Main axis: the original sequence; each token is represented with multidimensional embedding
  - Meta axes: supplementary streams of metatokens, encoding some semantic abstractions, aligned (via ordering) with the tokens from the main axis. Tokens from meta axes are also represented with multidimensional embedding
  
- Each main token could now be interpreted within a grid of metadata: not just “what preceded or what comes next?” but “how does this relate to other concepts?”
  
- Transformers would be trained to:
  - Predict (generate) tokens along the main axis, leveraging tokens from meta axes on top of preceding tokens from the main axis
  - Predict (generate) tokens along meta axes
    
- The meta sequences can be generated: 
  - Provided by human as rules that can be efficiently run over main sequence
  - Provided by symbolic algorithm, that is computationally not implementable in Transformer
  - Distilled from the Transformer as a code that can be efficiently applied over the main sequence
      
The intuition for grid-like representation is in 1) its alignment with Transformer’s natural concept of sequence and 2) its expressiveness. On latter, this representation intuitively captures the cases like:
- Assigning additional information for main tokens, e.g. this token is part of lexeme, etc.
- Grouping main tokens into a high level concepts
- Introducing hierarchy of concepts through multiple meta axes


Figure 1. Illustration of grid of meta sequences

The research is agnostic to the underlying algorithm, e.g. Transformer vs. LSTM. It is concept of "meta sequence" that matters in this proposal and it can be applied for other than Transformer architectures.

## Why This Matters
The introduction of metasequences is expected to render the benefits outlined in the Table below. Both benefits and rationale should be verified.

Benefit | Rationale
|---|---|
_Efficiency (e.g. reduced resources for training and faster training time)_ 
Boost Transformer base model training efficiency | The model’s capacity wouldn’t be spent on generalization of massive a priori knowledge (e.g. part of speech, lexemes) if they were already injected as meta sequences
Reduce Transformer’s learning requirement for new data | Transformer can meaningfully recycle already known (i.e. used in training) data if it is enriched by accompanying meta sequences
Introduce Transformers' capability for continuous self-improving via tight feedback loop | The model can generate new useful metasequences (e.g. via generating scalable code to create meta sequence for a main sequence) that can play role of generalization and memorization
Introduce Transformers' capability for modular expansion | Meta sequences can be used as natural way to gradually evolve transformer without retraining it from scratch
Finding Transformer’s architecture “sweet spot” | Meta sequence architecture introduces additional flexibility that can be exploit for optimal allocation of computing budget between the model’s elements
_Effectiveness (e.g. better quality of the output)_
Better interpretability and alignment control | Explicitly modeled concepts in meta sequences are additional levers for model’s alignment and interpretability control
Adopt hierarchical reasoning | The explicit modeling of relationship between low-level tokens and high-level concepts allows better Transformer’s reasoning (e.g. planning) because of leveraging data symmetries
Improve accuracy of Transformer’s inference | The metasequence (e.g. when it is generated through symbolic calculation or provided as human input) will complement Transformer’s capability to generalize, naturally constrained due to Transformer’s statistical learning foundation
Provide more flexibility to internal reasoning process through inference time chain-of-thought process within model

## 🧪 Promising early results. Yet not tested at full
The research is in progress but the first tests suggest it is a promising direction: the Transformer benefits from meta axes, showing improved token prediction accuracy (measured across main axis) and speed up training (see charts below). This observation supports the first benefit from the table and is necessary (though not sufficient) for other benefits to hold.

## 📂 Structure
- `model/` — Core implementation
- `data/` — Sample toy datasets
- `notebooks/` — Experiment notebooks
- `results/` — Charts and logs
- 
Experiment design overview:
- Data set is the fairy tales corpus provided by Kaggle
- Main axis’ tokens comprise of individual letters
- Baseline Transformer is implementation shared by Andrew Karpathy
- Secondary axis’ tokens represent commonly used lexemes that the main token is part of. Commonly used lexemes are predefined
- Tertiary axis’ tokens represent part of speech for the word that the main token is part of. Part of speech is determined via NLTK package
- Transformer extension to accommodate meta axes is built through inheriting new classes from baseline transformer classes
- Performance improvement is measured as difference in prediction loss for baseline and extended transformer through multiple training runs with different hyper parameters. See diagrams below that illustrate performance improvements
- No hyper parameters optimizations as well as Transformer architecture optimizations have been performed

## 🤝 Collaboration
Open to contributions! Let’s push this forward together.

## 🔗 Links
- [Discussion Thread on Reddit](#)
