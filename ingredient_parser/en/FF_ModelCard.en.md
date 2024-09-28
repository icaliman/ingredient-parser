# Foundation Foods Model Card

## Model Details

### Person or Organisation

<https://github.com/strangetom>

### Model Date and Version

Date: Sep 2024

Version: The model version is the same has the `ingredient_parser_nlp` package version.

Filename: ff_model.en.crfsuite

### Model Type

Natural language model for labelling name tokens in a recipe ingredient sentence as a foundation food or not..

The model is a Conditional Random Fields (CRF) model, implemented using [pycrfsuite](https://github.com/scrapinghub/python-crfsuite). A pre-processing step is required before a sentence can be presented to the model, which performs a number of text normalisation operations. See [preprocess.py](https://github.com/strangetom/ingredient-parser/blob/master/ingredient_parser/en/preprocess.py).

### License

The model, including the training data and training scripts and python package, are released under an [MIT License](https://github.com/strangetom/ingredient-parser/blob/master/LICENSE).

### Questions or Comments

Questions or comments can be raised by opening an issue on GitHub: https://github.com/strangetom/ingredient-parser/issues.

## Intended Use

The foundation foods model identifies foundation foods from English language ingredient sentences.

### Primary Intended Uses

- Label tokens in English language recipe ingredient sentences with one of the following labels:
  - FF: Foundation Food
  - NF: Not foundation food

### Primary Intended Users

- Developers and users of recipe management software or services

### Out-of-Scope Uses

- Token labelling for sentences in languages other than English.
- Token labelling for sentences written in scripts other than the Latin alphabet using standard special characters.
- Labelling of token sequences that aren't ingredient names.
- Labelling multiple sentences simultaneously. Attempting to pass a string containing multiple sentences is not supported and has not been tested.

## Limitations

The model has been trained on datasets that have limitations.

- The New York Times dataset contains sentences that largely follow a consistent style, use US customary units, and often refer to ingredients or brands found only in the USA.
- The Cookstr dataset contains sentences that use US customary units as the primary unit, and often refer to ingredients or brands found only in the USA. Sentences often include amours in multiple unit formats (US customary, metric). The ingredient sentences are often quite long and complex.
- The BBC Food dataset contains sentences that use metric units as the primary unit, but also often have the amounts in US customary units too. The ingredient sentences are generally quite simple and consistent in their structure.
- The AllRecipes dataset contains sentences that usually use US customary units and often reference US brand names or branded products. The ingredient sentences are generally quite simple and consistent in their structure.

Long sentences increase the likelihood of the model mislabelling tokens.

## Metrics

Word level accuracy measures the percentage of words in the evaluation data that were correctly labelled.

Sentence level accuracy measures the percentage of ingredient sentences where all words were correctly labelled.

## Training and Evaluation Data

There are 4 datasets used to train and evaluate model performance.

1. New York Times, originally found at https://github.com/nytimes/ingredient-phrase-tagger.

   The first 30,000 sentences are used in the training and evaluation of the model.

2. Cookstr, originally found as part of https://archive.org/details/recipes-en-201706.

   The first 15,000 sentences are used in the training and evaluation of the model.

3. BBC Food, originally found as part of https://archive.org/details/recipes-en-201706.

   The first 15,000 sentences are used in the training and evaluation of the model.

4. AllRecipes, originally found as part of https://archive.org/details/recipes-en-201706.

   The first 15,000 sentences are used in the training and evaluation of the model.

All datasets have been through extensive cleaning to make the data consistent. The cleaned versions of the data are found in the repository for the ingredient_parser_nlp package: https://github.com/strangetom/ingredient-parser

The model is trained on a randomised set of 80% of the total data, and evaluated on the remaining 20%.

## Quantitative Analysis

The model has the following performance metrics:

| Word level accuracy | Sentence level accuracy |
| ------------------- | ----------------------- |
| 98.73 ± 0.22%       | 97.75 ± 0.32%           |

These metrics were determined by executing 20 training/evaluation cycles and calculating the mean and standard deviation for the two metrics across all cycles. The uncertainty values provided represent the 99.7% confidence bounds (i.e. 3x standard deviation). The uncertainty is due to the randomisation of the selection of training and evaluation data whenever the model is trained.

## Ethical Considerations

There are no known ethical considerations related to this model.

## Caveats and Recommendations

The model is under active development and the stated performance is likely to change between releases. Best efforts will be made to keep this model card up to date.