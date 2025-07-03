# Metadata Enhanced Transformer

## Brief

**As-Is | Plain data based Transformer**

1|2|3|4
|--|--|--|--|
Token1|Token2|Token3|Token...

**Proposal | Metadata-augmented Transformer**

1|2|3|4
|--|--|--|--|
Token1|Token2|Token3|Token...
Metatoken1|Metatoken2|Metatoken3|Metatoken...
MetatokenA|MetatokenB|MetatokenC|Metatoken...

- Metadata should be valuable and meaningful but not perfect. Matching metadata to data should be computationally efficient. 
- Plain data remains the same. Examples of metadata used in PoC: morphemes, part of speech. PoC's plain data is alphanumeric characters.
- Requires slight adjustments to LLM architecture to process a few streams of tokens (multiple strategies possible).

## Trials results

![alt_text](https://docs.google.com/spreadsheets/d/e/2PACX-1vT7s-y23MXmYuxQs6TnNRXrJcmdetSjpsCpJjWv0MZP3W5f9HLT1pEVvnSb3jt2wDTLhF4hKjd02h0Z/pubchart?oid=1043107846&format=image)

![alt_text](https://docs.google.com/spreadsheets/d/e/2PACX-1vT7s-y23MXmYuxQs6TnNRXrJcmdetSjpsCpJjWv0MZP3W5f9HLT1pEVvnSb3jt2wDTLhF4hKjd02h0Z/pubchart?oid=89625722&format=image)

![alt_text](https://docs.google.com/spreadsheets/d/e/2PACX-1vT7s-y23MXmYuxQs6TnNRXrJcmdetSjpsCpJjWv0MZP3W5f9HLT1pEVvnSb3jt2wDTLhF4hKjd02h0Z/pubchart?oid=1906684737&format=image)

## Potential other benefits
- Improved interpretability and model alignment control
- RL via feedback loop and data recycling - model produces metadata and is re-trained w/ same plain data augmented w metadata
- Improved reasoning capabilities through "branching" inference in metadata space

## Open questions
- Optimal architecture
- Valuable meta data origination incl. RL
- Proof-of-concept at industry grade models
  
## Experiment overview
- Plain data set - fairy tales corpus from Kaggle; stored in archive.zip
- Transformer implementation is based on A. Karpathy's; it is character based
- First metadata set - list of often used morphemes
- Second metadata set - part of speech, determined by NLTK function
- Comparable models size via hyperparameters adjustment
