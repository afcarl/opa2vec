# Ontologies Plus Annotations to Vectors: OPA2Vec
## Introduction
OPA2Vec is a tool that can be used to produce feature vectors for biological entities from an ontology. OPA2Vec uses mainly metadata from the ontology in the form of annotation properties as the main source of data. It also uses formal ontology axioms as well as entity-concept associations as sources of information. 
This document provides instructions on how to run OPA2Vec as a tool and contains also a detailed documentation of the implementation of OPA2Vec for users willing to change the code according to their needs which is quite easy.
## Pre-requisites
OPA2Vec implementation uses Groovy with Grape for dependency management (http://docs.groovy-lang.org/latest/html/documentation/grape.html), Python and Perl. No other programs are required to run it.
## Running OPA2Vec
- Create a new directory and name it OPA2Vec.
- Download all the provided files from this repository to the OPA2Vec directory.
- In the terminal, run 
```
python runOPA2Vec.py "ontology file" "association file" -annotations "URI1,URI2" -pretrained "filename" -embedsize N -windsize N -mincount N -model sg/cbow  -entities "filename"
```
where the following are mandatory arguments:

 - **ontology file**            File containing ontology in owl format
  
 - **association file**         File containing entity class associations
  

You can also specify the following optional arguments:

 -  -h, --help              show this help message and exit
 
 -  **-annotations [metadata annotations]**
 List of full URIs of annotation properties to be included in metadata separated by a comma . Use 'all' for all annotation properties (default) or 'none' for no annotation property

 -  **-embedsize [embedding size]**  
                                Size of obtained vectors

 - **-windsize [window size]**  
                                Window size for word2vec model

  - **-mincount [min count]**  
                                Minimum count value for word2vec model
  - **-model [model]**         
  Preferred word2vec architecture, sg or cbow
 
  - **-pretrained [pre-trained model]**
  Pre-trained word2vec model for background knowledge. If no pre-trained model is specified, the program will assume you have downloaded the default pre-trained model from http://bio2vec.net/data/pubmed_model/ (Please download all three files)
 
  
In more detail:
- **"ontology file"** is the path to the file containing the ontology in owl format.(e.g. PhenomeNet onotology)
- **"association file"** is the path to the file containing the entity-concept associations (e.g. disease-phenotype associations).  
    + If more than one association file is needed, concatenate them into one file.
    + The ontology classes in the association file should be represented with their full URIs, e.g: .
    +Ideally, the association file should contain two columns in each line: the entity (e.g. protein) and the full URI of the ontology class (e.g. GO function) it is annotated with separated by one space as shown in the file *SampleAssociationFile.lst*. 

- **"-annotations"** is the optional parameter used to specify the list of the metada annotation properties (with their full URIs) you would like to use.E.g:<http://purl.obolibrary.org/obo/IAO_0000115>. You can also choose to use "all" annotation properties (default) or "none".
- **"-entities file"** is the optional file containing the list of biological entities for which you would like to get the feature vectors (each entity in a separate line). If no file is specified the program will output vectors for all enitities and classes in the corpus.
- **"-pretrained"** is the optional name of the pre-trained word2vec model. You can pre-train word2vec using the corpus of your choice (Wikipedia, PubMed, ...) and use it to run OPA2Vec by providing it as input. By default, our program uses a model pre-trained on PubMed. If you choose to use the default model, please download it from  http://bio2vec.net/data/pubmed_model/, otherwise the program will raise an error. 
### Output
The script should create a file *AllVectorResults.lst* (among other intermediate files) that contains vector representations for all classes specified in the "entities file" (or all classes if no file is provided). An example of what *AllVectorResults.lst* should look like is shown in *SampleVectors.lst*.

## Related work
Please refer to the following  for related work:
- Smaili, F. Z. et al. (2018). Onto2vec: joint vector-based representation of
biological entities and their ontology-based annotations. arXiv preprint
arXiv:1802.00864.
- https://github.com/bio-ontology-research-group/onto2vec
## Final notes
For any comments or help needed with how to run OPA2Vec, please send an email to: fzohrasmaili@gmail.com
