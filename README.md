# Introduction
This document is included in the 'One-to-One or One-to-Many? Suggesting Extract Class Refactoring Opportunities with Intra-class Dependency Hypergraph Neural Network' distribution, which we will refer to as HECS. This is to distinguish the recommended implementation of this Extract Class refactoring from other implementations. In this document, the environment required to make and use the HECS tool is described. Some hints about the installation environment are here, but users need to find complete instructions from other sources. They give a more detailed description of their tools and instructions for using them. Our main environment is located on a computer with windows (windows 11) operating system. The fundamentals should be similar for other platforms, although the way in which the environment is configured will be different. What do I mean by environment? For example, to run python code you will need to install a python interpreter, and if you want to use pre-trained model you will need torch.

# HECS
/src: The code files which is involved in the experiment \
/AccEval: Graph Representation of AccEval \
/data_demo: relevant data of the example involved in Section 2 of the paper \
/RQ3: the questionnaire and case study results \
/tool:  a Visual Studio Code (VSCode) extension of hecs 

# Technique
## pre-trained model
CodeBERT GraphCodeBERT CodeGPT CodeT5 CoTexT PLBART

# Requirement
## CodeBERT, GraphCodeBERT, CodeGPT, CodeT5, CoTexT, PLBART
python3(>=3.6) \
we use python 3.9\
torch transformers \
we use torch(1.12.0) and transformers(4.20.1)\
pre-trained model link: \
CodeBERT: https://huggingface.co/microsoft/codebert-base \
CodeGPT: https://huggingface.co/microsoft/CodeGPT-small-java-adaptedGPT2 \
GraphCodeBERT: https://huggingface.co/microsoft/graphcodebert-base \
CodeT5: https://huggingface.co/Salesforce/codet5-base-multi-sum \
CoTexT: https://huggingface.co/razent/cotext-2-cc \
PLBART: https://huggingface.co/uclanlp/plbart-base

## hyper-parameter settings

| Embedding Technique |                   Hyper-parameter settings                   |
| :-----------------: | :----------------------------------------------------------: |
|      CodeBERT       | train\_batch\_size=2048, embeddings\_size =768, learning\_rate=5e-4, max\_position\_length=512 |
|    GraphCodeBERT    | train\_batch\_size=1024, embeddings\_size =768, learning\_rate=2e-4, max\_sequence\_length=512 |
|       CodeGPT       |      embeddings\_size =768, max\_position\_length=1024       |
|       CodeT5        | train\_batch\_size=1024, embeddings\_size =768, learning\_rate=2e-4, max\_sequence\_length=512 |
|       PLBART        | train\_batch\_size=2048, embeddings\_size =768, dropout=0.1  |
|       CoTexT        | train\_batch\_size=128, embeddings\_size =768, learning\_rate=0.001, model\_parallelism=2, input\_length=1024 |

# Quickstart

##  Training phase

> step1: we extract intra-class dependency graphs from both training samples and transform these into hypergraphs.

path: `src/DataPreprocessing/`

> step 2: nodes in these hypergraphs are assigned with attributes with pre-trained code model

path: `src/DataPreprocessing/pre-trained model`

> step 3: these attributed hypergraphs are fed into an enhanced hypergraph neural network for the purpose of training.

path: `src/GraphLearning/`

##  Detecton phase

> The detection phase first constructs attributed hypergraph through hypergraph construction and node attribute generation. Based on constructed attributed hypergraphs, the detection phase further conducts refactoring opportunity suggestion via hierarchical model invocation and LLM-based pre-condition verification. 

path: `src/RefactoringOpportunitySuggestion/`

# Datasets

AccEval: [Tsantalis et al's dataset](https://refactoring.encs.concordia.ca/oracle/tool-refactorings/*All%20Refactorings/TP/Extract%20Class) 

HumanEval: [Xerces](https://github.com/apache/xerces2-j), [GanttProjects](https://github.com/bardsoftware/ganttproject)
