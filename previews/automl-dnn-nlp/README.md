# AutoML DNN-NLP

## Overview
The advent of the [transformer architecture](https://arxiv.org/abs/1706.03762) and the later development of [BERT](https://arxiv.org/abs/1810.04805) has greatly boosted machine learning's performance on NLP tasks. Now, you can take the advantage of BERT and apply this powerful pretrained model on you own tasks with Azure Machine Learning AutoML NLP capability. 

Currently, our AutoML DNN-NLP service supports three scenarios: 
* multi-class classification
  * There are multiple possible classes and each sample can be classified as exactly one class. The task is to predict the correct class for each sample.
* multi-label classification
  * There are multiple possible classes and each sample can be assigned any number of classes. The task is to predict all the classes for each sample.
* Named Entity Recognition (NER)
  * There are multiple possible tags for tokens in sequences. The task is to predict the tags for all the tokens for each sequence.

## Installation and set up

* Azure subscription. If you don't have an Azure subscription, , sign up to try the [free or paid version of Azure Machine Learning](https://azure.microsoft.com/free/) today.
* A Workspace with GPUs available. Please check [this page](https://docs.microsoft.com/en-us/azure/virtual-machines/sizes-gpu) for more details of GPU instances provided by Azure
* In order to utilize this new feature with our SDK, please follow the setup instruction on [this page](https://github.com/ZeratuuLL/azureml-examples/tree/main/python-sdk/tutorials/automl-with-azureml). That would be enough to start AutoML DNN-NLP runs with a jupyter notebook. If you would like to explore more about our DNN-NLP offering, you can do so by running ``` pip install azureml-automl-dnn-nlp ```

## Getting started

### Quick Start
For a quick start with a live demo notebook, please refer to [this example notebook](https://github.com/ZeratuuLL/azureml-examples/tree/lifengwei/multiclass-notebook/python-sdk/tutorials/automl-with-azureml/automl-dnn-nlp) for a complete AutoML DNN-NLP run for multi-class scenario. You can also learn how to run multi-label and NER tasks with code snippets example and sample data.

### General procedure
For the general procedure of setting AutoML DNN-NLP run, all three scenarios share similar steps:
1. Retrieve workspace and create/choose compute instance.
2. Prepare and register datasets.
3. Set `AutoMLConfig` accordingly.
4. Submit the run. 
5. Check result with SDK or UI. 

Step 1, 4 and 5 are exactly the same as general AutoML runs. As for step 3, you **only need to choose the preferred `task` parameter based on your scenario and we will take care of the rest**.

For more details and examples for how to set `AutoMLConfig` and prepare datasets in required format, please check docs for [multi-class](./docs/multi-class.md), [multi-label](./docs/multi-label.md), and [NER](./docs/ner.md)

## Other features

### Multilingual support
AutoML DNN-NLP service supports 104 different languages. You can specify the language by language code, or let DNN-NLP auto detect the correct language for you. For the full list of supported languages and their language code, please [check this page](https://docs.microsoft.com/en-us/python/api/azureml-automl-core/azureml.automl.core.constants.textdnnlanguages?view=azure-ml-py#supported-----afr----afrikaans----ara----arabic----arg----aragonese----ast----asturian----azb----south-azerbaijani----aze----azerbaijani----bak----bashkir----bar----bavarian----bel----belarusian----ben----bengali----bos----bosnian----bpy----bishnupriya----bre----breton----bul----bulgarian----cat----catalan----ceb----cebuano----ces----czech----che----chechen----chv----chuvash----cym----welsh----dan----danish----deu----german----ell----greek----eng----english----est----estonian----eus----basque----fas----persian----fin----finnish----fra----french----fry----western-frisian----gle----irish----glg----galician----guj----gujarati----hat----haitian----hbs----serbo-croatian----heb----hebrew----hin----hindi----hrv----croatian----hun----hungarian----hye----armenian----ido----ido----ind----indonesian----isl----icelandic----ita----italian----jav----javanese----jpn----japanese----kan----kannada----kat----georgian----kaz----kazakh----kir----kirghiz----kor----korean----lah----western-punjabi----lat----latin----lav----latvian----lit----lithuanian----lmo----lombard----ltz----luxembourgish----mal----malayalam----mar----marathi----min----minangkabau----mkd----macedonian----mlg----malagasy----mon----mongolian----msa----malay----mul----multilingual---collection-of-all-supporting-languages----mya----burmese----nds----low-saxon----nep----nepali----new----newar----nld----dutch----nno----norwegian-nynorsk----nob----norwegian-bokm-l----oci----occitan----pan----punjabi----pms----piedmontese----pol----polish----por----portuguese----ron----romanian----rus----russian----scn----sicilian----sco----scots----slk----slovak----slv----slovenian----spa----spanish----sqi----albanian----srp----serbian----sun----sundanese----swa----swahili----swe----swedish----tam----tamil----tat----tatar----tel----telugu----tgk----tajik----tgl----tagalog----tha----thai----tur----turkish----ukr----ukrainian----urd----urdu----uzb----uzbek----vie----vietnamese----vol----volap-k----war----waray-waray----yor----yoruba----zho----chinese--)

To select the language, you need to set

```
from azureml.automl.core.featurization import FeaturizationConfig
featurization_config = FeaturizationConfig(dataset_language='{your language code}')
```

And then pass it into `AutoMLConfig`

```
automl_config = AutoMLConfig("featurization": featurization_config, **other_settings)
```

To enable auto language detection, you can simply do
```
automl_config = AutoMLConfig("featurization": "auto", **other_settings)
```

## Coming Soon

### Start training with UI

We are actively working on UI supports to enable everyone to create use AutoML DNN-NLP feature through simple UI operations!

### Distributed Training
We are working on applying [horovod](https://github.com/horovod/horovod) to support stable, high-performance distributed learning for all three scenarios.

## Contact Us

For any questions, bugs and requests of new features, please contact us at [AutoMLText@microsoft.com](mailto:AutoMLText@microsoft.com)
