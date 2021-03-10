# Food - Disease Relation Extraction dataset
The FoodDisease dataset contains 608 sentences annotated for the existence of _cause_ and _treat_ relations between food and disease entities. The sentences were extracted from abstracts of biomedical research papers published in PubMed.

[BuTTER](https://github.com/gjorgjinac/butter) [1] and [SABER](https://baderlab.github.io/saber/) [2] were used for finding the food and disease entities in each abstract. BuTTER is a Named Entity Recognition (NER) method which extracts food entities from raw text, while SABER is a biomedical NER tool which extracts disease entities. Both methods are based on Bidirectional Long Short-Term Memory and Conditional Random Fields. In particular, we used the lexical lemmatized BuTTER model introduced in [1], and the [DISO pretrained model](https://baderlab.github.io/saber/resources/) from the SABER tool.
The SABER tool also performs Named Entity Linking (NEL), so that some of the extracted disease entities are linked to concepts in the Disease Ontology.

The abstracts were filtered so that only sentences which contain at least one food and one disease entity were kept. The entities in each sentence were then manually checked and corrected in order to remove false positives and complete partial matches. Removing the false positive entities means that the tokens that were incorrectly extracted as food or disease entities by the BuTTER and SABER methods were discarded. Completing partial matches entails adding the missing words in entities which should contain multiple words, but some of them were not captured by the automatic annotators. 
Finally, each sentence was assigned binary labels to indicate if the _cause_ and _treat_ relations are present.

Each sample in the dataset contains:
* food_entity: the name of the food entity extracted by BuTTER and manually curated
* disease_entity: the name of the disease entity extracted by SABER and manually curated
* sentence: the sentence in which the food and disease entities co-occur
* disease_doid: the id of the disease in the Disease Ontology, as extracted by SABER
* is_cause: binary indicator of the existence of the _cause_ relation between the food and disease entities
* is_treat: binary indicator of the existence of the _treat_ relation between the food and disease entities

All fields except disease_doid are non-nullable.


[1] Gjorgjina Cenikj, Gorjan Popovski, Riste Stojanov, Barbara Koroušić Seljak, and Tome Eftimov. 2020. BuTTER: BidirecTional LSTM for Food Named-Entity Recognition. In Proc. Big Food and Nutrition Data Management and Analysis at IEEE BigData 2020, Atlanta, USA.

[2] John Giorgi and Gary Bader. 2019. Towards reliable named entity recognition in the biomedical domain. bioRxiv