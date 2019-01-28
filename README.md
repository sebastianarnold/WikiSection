# WikiSection Dataset

This dataset contains 38k full-text documents from English and German Wikipedia annotated with section segments. Each segment contains two labels: the original unfolded section heading given by the Wikipedia editor (e.g. `Treatment | Surgery`), and a normalized section class label (e.g. `disease.treatment`).

The WikiSection task is to assign each sentence in the document a corresponding section class in which the sentence appears. The document text itself does not contain structure information, such as sections, subsections, paragraphs or headlines. Newline characters are included and occur between sections as well as inside sections.

The documents originate from Wikipedia dumps avaliable as CC BY-SA 3.0 at [dumps.wikimedia.org/enwiki/20180101/](https://dumps.wikimedia.org/enwiki/20180101/) (English) and [dumps.wikimedia.org/dewiki/20180101/](https://dumps.wikimedia.org/dewiki/20180101/) (German). The data sets are filtered by instances of Wikidata classes [Q12136](https://www.wikidata.org/wiki/Q12136) (disease) and [Q515](https://www.wikidata.org/wiki/Q515) (city). Datasets are randomized and split into 70% training, 10% validation and 20% test documents.

## Data Set Overview

The following table shows the characteristics of the four subsets:

| dataset     | **en_disease** | **de_disease** | **en_city** | **de_city** | **total** |
|-------------|---------------:|---------------:|------------:|------------:|----------:|
| language    |     English    |     German     |   English   |    German   |           |
| instanceof  |     Q12136     |     Q12136     |     Q515    |     Q515    |           |
|             |                |                |             |             |           |
| # docs      |          3,590 |          2,323 |      19,539 |      12,537 |   **38k** |
| # sections  |         27,838 |         14,784 |     133,642 |      65,907 |  **242k** |
| # sentences |        209,885 |        106,198 |   1,104,619 |     500,100 |  **1.9M** |
|             |                |                |             |             |           |
| # heaadings |          ~8.5k |          ~6.1k |      ~23.0k |      ~12.2k |           |
| # classes   |             27 |             25 |          30 |          27 |           |
| coverage    |          94.6% |          89.5% |       96.6% |       96.1% |           |

The numbers for docs, sections and sentences denote the total number of instances in the subset. *headlines* denotes the number of distinct section and subsection headings among documents. *classes* denotes the number of class labels after normalization and pruning the long tail. *coverage* denotes the proportion of sections covered by the class labels. The remaining sections are given the class `other`.

## Data Format

The WikiSection dataset is provided in JSON format.

| Field          | Description                                              |
|:---------------|----------------------------------------------------------|
| `type`         | `city` or `disease`                                      |
| `title`        | Title of the article                                     |
| `abstract`     | Full text of the article abstract                        |
| `text`         | Full text of the document body without abstract, headings and structure elements. Format: utf-8, not tokenized, includes newlines |
| `annotations`  | List of sections                                         |
| `class`        | `SectionAnnotation`                                      |
| `begin`        | Begin offset in the document. Format: number of characters starting at 0. Newlines and escaped symbols count as one character |
| `length`       | Length of the section. Format: number of characters      |
| `sectionHeading` | Original heading of the section. Nested headings are unfolded and segmented by ` | `. |
| `sectionLabel` | Normalized class label                                   |

Alternatively, we provide the same data in a REF format that consists of one file per document and one sentence per line.

### Example JSON

```JSON 
{
  "id" : "https://en.wikipedia.org/wiki/Autoimmune_polyendocrine_syndrome",
  "type" : "disease",
  "title" : "Autoimmune polyendocrine syndrome",
  "abstract" : "Autoimmune polyendocrine syndromes (APSs), also called [...]",
  "text" : "Each \"type\" of this condition has a different cause, in terms of [...]",
  "annotations" : [ {
    "class" : "SectionAnnotation",
    "begin" : 0,
    "length" : 238,
    "sectionHeading" : "Cause",
    "sectionLabel" : "disease.cause"
  }, ... ]
}
```

## Table of Class Labels

| **en_disease**  | **de_disease**  | **en_city**           | **de_city**           |
|-----------------|-----------------|-----------------------|-----------------------|
| cause           | definition      | architecture          | architektur           |
| classification  | diagnose        | climate               | bildung               |
| complication    | epidemiologie   | crime                 | demografie            |
| culture         | fauna           | culture               | erholung              |
| diagnosis       | forschung       | demography            | etymologie            |
| epidemiology    | genetik         | district              | gemeinde              |
| etymology       | geographie      | economics             | gemeindepartnerschaft |
| fauna           | geschichte      | education             | geographie            |
| genetics        | infektion       | environment           | geschichte            |
| geography       | kategorisierung | etymology             | infrastruktur         |
| history         | klinik          | facility              | kirche                |
| infection       | komplikation    | faith                 | klima                 |
| management      | mensch          | geography             | kriminalität          |
| mechanism       | organe          | health                | kultur                |
| medication      | pathologie      | history               | menschen              |
| pathology       | prävalenz       | infrastructure        | politik               |
| pathophysiology | prognose        | international_affairs | presse                |
| prevention      | risiko          | law                   | regierung             |
| prognosis       | symptom         | media                 | religion              |
| research        | terminologie    | overview              | sport                 |
| risk            | therapie        | people                | stadtlandschaft       |
| screening       | ursache         | politics              | stadtviertel          |
| surgery         | verlauf         | recreation            | tourismus             |
| symptom         | vorbeugung      | science               | überblick             |
| tomography      | sonstiges       | sights                | verkehr               |
| treatment       |                 | society               | wirtschaft            |
| other           |                 | sport                 | sonstiges             |
|                 |                 | tourism               |                       |
|                 |                 | transport             |                       |
|                 |                 | other                 |                       |

## Credit

If you use this dataset for research, please cite:

Sebastian Arnold, Rudolf Schneider, Philippe Cudré-Mauroux, Felix A. Gers and Alexander Löser. "SECTOR: A Neural Model for Coherent Topic Segmentation and Classification." Transactions of the Association for Computational Linguistics (2019).

## License

This dataset uses material from Wikipedia articles listed in the SOURCES file, which are released under the [Creative Commons Attribution-ShareAlike 3.0 Unported License](https://creativecommons.org/licenses/by-sa/3.0/">). You should have received a copy of the license along with this
work. If not, see [http://creativecommons.org/licenses/by-sa/3.0/].
