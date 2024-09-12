## Name 
MIRA 

## Full title 
MIRA - A Knowledge Graph for Social Demography Hypotheses and Findings.

## Application domain
Semantic web, Graphs, Natural Language Processing 

## Keywords 
Social Demography, Knowledge Graph, Scientific Hypotheses, Information Extraction 

## Description 
This github presents the MIRA-KG, a knowledge graph designed to capture hypotheses and findings in social demography research. The resource aids researchers in understanding the trends and patterns revealed in social demography, and use them to discover biases, discover knowledge, and derive novel questions.

## Code repository
https://github.com/muhai-project/mira

## Overview 

In the research workflow of a social historian or social demographer, research questions commonly include (i) descriptive questions, (ii) comparative questions, and (iii) explanatory questions. Here, each question is answered based on the output from a previous question or dataset, see the image below. An example workflow, and how such a workflow can be made more FAIR, is shown below. 

![Example annotation](figures/FAIRifying-SD.png)

In social demography, work has been done formally describing observational data, such as census data hosted as linked data at the International Institute of
Social History (IISH). To the best of our knowledge, no studies formalise knowledge such as hypotheses and findings on social demography, whereas these are important in each of the
steps of the scientific workflow of a social historian (see declarative/procedural knowledge in the figure above). The research process, hypotheses and findings are mostly written up in scientific documents
in natural language, which can be ambiguous and imprecise. Such fields can thus benefit from adopting the FAIR data principles, to reduce unclarity and ambiguity in the research workflow of a social demographer. 

The [MIRA ontology](https://w3id.org/mira/ontology/) describes this process: it links datasets of observations to research questions, to accommodate the research workflow of a social demographer/social historian towards more reusable, reproducible research. We also populate the ontology with structured research questions on health inequality, extracted from abstracts of research papers, and is published on [Zenodo](https://doi.org/10.5281/zenodo.10286846), and queriable via a [SPARQL endpoint](
https://api.druid.datalegend.net/datasets/lisestork/MIRA-KG/services/MIRA-KG/sparql).

This [github](https://github.com/muhai-project/mira/) contains the ontology, example annotations, scripts to produce structured annotations automatically from paper abstracts (explanatory questions and metadata of evidence used to answer the RQs), and SHACL shapes for the validation of generated annotations.


### Usage examples:

SPARQL queries can be found here: [https://github.com/muhai-project/mira/tree/main/queries](https://github.com/muhai-project/mira/tree/main/queries)
An example query is shown below: 

# CQ 1 what is the evidence for a specific claim (which descriptive statistics, based on what type of sample?) 

```
PREFIX sem: <http://semanticweb.cs.vu.nl/2009/11/sem/>
PREFIX mira: <https://w3id.org/mira/ontology/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX sio: <http://semanticscience.org/resource/>
PREFIX qb: <http://purl.org/linked-data/cube#>
PREFIX time: <http://www.w3.org/2006/time#>
PREFIX gn: <http://www.geonames.org/ontology#>
PREFIX stato: <http://purl.obolibrary.org/obo/> 
PREFIX mesh: <http://purl.bioontology.org/ontology/MESH/>
PREFIX wgs84_pos: <http://www.w3.org/2003/01/geo/wgs84_pos#>

select ?inf_cont_ent1 ?inf_cont_ent2 ?ice1_type ?ice2_type 
        ?subject ?begin ?end ?name ?lat ?long where { 
    ?comp a mira:Comparison . 
        mira:hasSubject ?inf_cont_ent1 ; #descriptive statistic
        mira:hasObject ?inf_cont_ent2 ; #descriptive statistic
        mira:hasRelation ?relation ; #relation between the two descriptive statistics
        mira:hasContext ?sample ;  #dataset used to calculate the statistics
        sio:SIO_000205 ?exp .
    ?exp mira:hasSubject/qb:concept/rdfs:label ?subject ; #what is the subject of the claim
         #the object of the claim is COVID-19 and Mortality
         mira:hasObject/qb:concept mesh:D000086382, stato:STATO_0000414 .
    ?inf_cont_ent1 sio:SIO_000332 ?component_property1 ; #what does the statistic measure
        rdf:type ?ice1_type . #what type of statistic (e.g., a mean)
    ?inf_cont_ent2 sio:SIO_000332 ?component_property2 ; #what does the statistic measure 
        rdf:type ?ice2_type . #what type of statistic (e.g., a mean)
    #what is the temporal and geographic coverage of the sample
    ?sample time:hasTime/time:hasBeginning/time:inXSDDate ?begin ;  #start time
        time:hasTime/time:hasEnd/time:inXSDDate ?end ; #end time
        #retrieve geonames metadata
        sem:hasPlace/gn:locatedIn ?gnId . 
        ?gnId gn:name ?name ;
            wgs84_pos:long ?long ; 
            wgs84_pos:lat ?lat . }
```

## Ontologies 
[ontology/ontology.ttl](https://github.com/muhai-project/mira/blob/main/ontology/ontology.ttl)

## License

This project is licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

## Citation

@InProceedings{10.1007/978-3-031-60635-9_12,
author="Stork, Lise and Zijdeman, Richard L. and Tiddi, Ilaria and ten Teije, Annette",
editor="Mero{\~{n}}o Pe{\~{n}}uela, Albert and Dimou, Anastasia and Troncy, Rapha{\"e}l and Hartig, Olaf and Acosta, Maribel and Alam, Mehwish and Paulheim, Heiko and Lisena, Pasquale",
title="Enabling Social Demography Research Using Semantic Technologies",
booktitle="The Semantic Web",
year="2024",
publisher="Springer Nature Switzerland",
address="Cham",
pages="199--216",
isbn="978-3-031-60635-9"
}

## DOI 
10.1007/978-3-031-60635-9_12, 
10.5281/zenodo.10286845

## Contact 
Lise Stork, l.stork@uva.nl

## Contributors
Lise Stork, Richard Zijdeman, Ilaria Tiddi, Annette ten Teije

## Owner 
muhai-project

## Owner type
Organization  

## Repository status 
Active 

## Acknowledgment
This work was funded by the European MUHAI project (Horizon 2020 research and innovation program) under grant agreement
number 951846. We thank Tobias Kuhn and Inès Blin for the insightful discussions that contributed to this work.


---

