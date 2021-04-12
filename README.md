
# The Bavard NLU Meta-Dataset

This intent classification dataset is a conglomeration of 6 task-oriented dialogue
datasets and intent classification datasets, all unified under a common, simple format. It is suitable for training
few-shot intent classification models as it spans 78 dialogue domains and has 1629
intents, with each intent having between 11 and 100 natural language
utterance examples. There are a total of 84212 utterances in the dataset. For more information on
how this dataset was curated, please see our
[article](https://figshare.com/articles/preprint/Announcing_The_New_Bavard_NLU_Intent_Service/14403380) announcing
the release of this dataset.

Here is a tabulation of the datasets used to create this dataset:

| Dataset Name | # Domains | # Intents | # Utterances | Original Paper |
| --- | --- | --- | --- | --- |
| [CLINC150](https://github.com/clinc/oos-eval/) | 10 | 150 | 15000 | [An Evaluation Dataset for Intent Classification and Out-of-Scope Prediction.](https://www.aclweb.org/anthology/D19-1131/) |
| [DSTC8-SGD](https://github.com/google-research-datasets/dstc8-schema-guided-dialogue/) | 46 | 1282 | 57582 | [Towards scalable multi-domain conversational agents: The schema-guided dialogue dataset.](https://ojs.aaai.org/index.php/AAAI/article/view/6394) |
| [HINT3](https://github.com/hellohaptik/HINT3/) | 3 | 59 | 1736 | [HINT3: Raising the Bar for Intent Detection in the Wild.](https://www.aclweb.org/anthology/2020.insights-1.16/) |
| [HWU64](https://github.com/xliuhw/NLU-Evaluation-Data/) | 14 | 51 | 4740 | [Benchmarking natural language understanding services for building conversational agents.](https://arxiv.org/abs/1903.05566) |
| [MultiWOZ 2.2](https://github.com/budzianowski/multiwoz/) | 3 | 27 | 1246 | [Multiwoz 2.2: A dialogue dataset with additional annotation corrections and state tracking baselines.](https://arxiv.org/abs/2007.12720) |
| [Taskmaster2](https://github.com/google-research-datasets/Taskmaster/) | 2 | 60 | 3908 | [Taskmaster-1: Toward a realistic and diverse dialog dataset.](https://arxiv.org/abs/1909.05358) |

## Dataset Organization

The dataset is accessible in the `./data` directory. Each source dataset has its own subdirectory, and each source
dataset's domain has its own json file under that subdirectory's dedicated `data` directory, for example:

```
data/
    dataset1/
        LICENSE.txt
        data/
            domainA.json
            domainB.json
            ...
    dataset2/
        LICENSE.txt
        data/
            domainC.json
            domainD.json
            ...
    ...
```

## The Data Format

Each json file contains a list of intent classification examples, which look like this:

```json
[
    {
        "intent": "rewards_balance",
        "utterance": "what is the amount of rewards points on my visa card",
        "origin": "CLINC150",
        "domain": "credit_cards"
    },
    {
        "intent": "CONSULT_START",
        "utterance": "Can you tell me what diet is perfect for me",
        "origin": "HINT3",
        "domain": "curekart"
    }
]
```

In this first example, the utterance "what is the amount of rewards points on my visa card" is associated with the
intent `rewards_balance`. The `origin` field indicates the dataset this example came from, and the `domain` field
indicates which task domain the example is associated with.

## Loading the Data

Here is a Python 3 example of loading all the data from all source datasets into a single array:

```python
import os
from glob import glob
import json

dataset = []
for domain_file_path in glob(os.path.join("data", "*", "data", "*.json")):
    with open(domain_file_path) as f:
        dataset += json.load(f)

print(len(dataset))
# 84212
```

## Licensing and Attribution

Here are links to the licenses of the original datasets. To respect those licenses, we release each derivative work of
each dataset in this meta-dataset under the same license as the original dataset. This should not inhibit use of our
meta-dataset as a whole. Each individual license should be consulted, but in general, this meta-dataset can be used for
any purpose, even commercially, so long as proper attribution is made, a link to the license is shared, and any
derivative works are open-sourced under the same license.

| Dataset Name | License URL |
| --- | --- |
| CLINC150 | [Attribution 3.0 Unported (CC BY 3.0)](https://github.com/clinc/oos-eval/blob/master/LICENSE) |
| DSTC8-SGD | [Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://github.com/google-research-datasets/dstc8-schema-guided-dialogue/blob/master/LICENSE.txt) |
| HINT3 | [Open Data Commons Open Database License (ODbL) v1.0](https://github.com/hellohaptik/HINT3/blob/master/LICENSE.md) |
| HWU64 | [Attribution 4.0 International (CC BY 4.0)](https://github.com/xliuhw/NLU-Evaluation-Data/blob/master/LICENSE) |
| MultiWOZ 2.2 | [MIT](https://github.com/budzianowski/multiwoz/blob/master/LICENSE) |
| Taskmaster2 | [Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/) |

To cite this dataset:

```
@misc{peterson_2021,
    title={Announcing The New Bavard NLU Intent Service},
    url={https://figshare.com/articles/preprint/Announcing_The_New_Bavard_NLU_Intent_Service/14403380/1},
    DOI={10.6084/m9.figshare.14403380.v1},
    publisher={figshare},
    author={Peterson, Evan},
    year={2021},
    month={Apr}
}
```

    