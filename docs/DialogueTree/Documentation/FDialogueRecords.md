---
layout: default
title: Dialogue Node Records Documentation
permalink: /DialogueTree/Documentation/FDialogueNodeRecords
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: FDialogueRecords
Struct used to extract the node visit "memory" of one or more dialogues. Useful for saving and loading. 

## Contents 
1. [**Data Attributes**](FDialogueRecords.md#1-data-attributes)
   * [**Records**](FDialogueRecords.md#records-blueprintreadonly)

## 1. Data Attributes
The following are the data attributes associated with the struct.
<br>

### Records (BlueprintReadOnly)
* **Type:** TMap<FName, FDialogueNodeVisits>
* **Access:** Public
* **Description:** Map of dialogue FNames to their records of visited nodes.
