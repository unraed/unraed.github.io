---
layout: default
title: Dialogue Node Visits Documentation
permalink: /DialogueTree/Documentation/FDialogueNodeVisits
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: FDialogueNodeVisits
Struct used to extract node visited data for a single dialogue. Primarily useful for saving/loading. 

## Contents 
1. [**Data Attributes**](FDialogueNodeVisits.md#1-data-attributes)
   * [**Dialogue FName**](FDialogueNodeVisits.md#dialogue-fname-blueprintreadonly)
   * [**VisitedNodeIndices**](FDialogueNodeVisits.md#visited-node-indices-blueprintreadonly-savegame)
  
## 1. Data Attributes
The following are the data attributes associated with the struct.
<br>

### Dialogue FName (BlueprintReadOnly) 
* **Type:** FName
* **Access:** Public
* **Description:** Name associated with the dialogue to which the visitation data belongs.
<br>

### Visited Node Indices (BlueprintReadOnly, SaveGame)
* **Type:** TSet\<int32\>
* **Access:** Public
* **Description:** Indices of nodes in the dialogue that have already been visited.
<br>

