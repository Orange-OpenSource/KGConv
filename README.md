# KGConv

KGConv is a large corpus of 71k English conversations where each question-answer pair is grounded in a Wikidata fact. Conversations contain on average 8.6 questions and each question is provided in several variants.

For a more complete description, see Q. Brabant, L. Rojas-Barahona, G. Lecorvé, C. Gardent. [KGConv, a Conversational Corpus grounded in Wikidata](https://arxiv.org/abs/2308.15298), 2023.

## How the data is structured


```
/data
├── labels.json
├── preferred_labels.json
├── root_neightbourhoods.json
├── template_library
├── complete_version
│	├── train
│	├── dev
│	└── test
└── simple_version
	├── train
	├── dev
	└── test
```

To see complete_version and simple_verison folders, you have to unzip the corresponding files in /data. The data is available in two versions, "complete" and "simple". The simple version is supposed to be easier to handle (I'm not 100% confident about that, tho); the complete version contain more details, such as the ID of the template used for each question. Each train, dev or test folder contains several json files. Each file corresponds to a theme and is structured as follows:


In the complete version:

```
{
	# each dialogue id is associated to a list of questions and answer
	"3445" : [
		{
			"triple" : ["subject_id", "property_id", "object_id"],
			"question_variants" : [
				{...}, # variants corresponding to one template
				{...}, # variants corresponding to another template
				...
			"answer" : "Stéphanie de Monaco" # the label of the triple's object
			]
		}, # first question and answer
		{...}, # second question and answer
		...
	]
}
```

In the simple version:

```
{
	# each dialogue id is associated to a list of questions and answer
	"3445" : [
		{
			"triple" : ["subject_id", "property_id", "object_id"],
			"out-of-context questions" : [...], # out-of-context variants of all questions from the complete version
			"in-context questions" : [...], # in-context variants of all questions from the complete version
			"synthetic in-context questions" : [...], # synthétic in-context variants of all questions from the complete version
			"answer" : "Stéphanie de Monaco" # the label of the triple's object
			]
		}, # first question and answer
		{...}, # second question and answer
		...
	]
}
```

Other files in the data folder:
* labels.json contains the labels associated to each (entity or property) identifier appearing in the conversations
* preferred_labels.json is the same as labels, but it only contains the default label for each identifier
* root_neighborhoods.json associates the root entity of each conversation to the triples from its neighbourhood in the (filtered) Wikidata knowledge graph
* template_library associates properties to templates



## Third party datasets

Our data include parts of the following datasets:
* simple_question_v2
  * can be downloaded [here](https://huggingface.co/datasets/simple_questions_v2)
  * described in Bordes et al. [Large-scale Simple Question Answering with Memory Networks](https://arxiv.org/abs/1506.02075), 2015.
* the zero-shot dataset
  * can be downloaded [here](http://nlp.cs.washington.edu/zeroshot/)
  * described in Levy et al. [Zero-Shot Relation Extraction via Reading Comprehension](https://aclanthology.org/K17-1034.pdf), CoNLL 2017.



## License

This corpus is distributed under CC-BY-4.0 license. See copyright_notice.txt for more details.
