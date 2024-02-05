---
layout: default
title: Dialogue Condition Documentation
permalink: /DialogueTree/Documentation/DialogueCondition
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Dialogue Condition 
Dialogue conditions are created as part of [**branch nodes**](DialogueNodes.md#branch-node) to specify the logic over which the node is to branch. In principle, conditions consist of a [**dialogue query**](DialogueQuery.md) and one or more sub-properties determined by the type of that query. 

## Contents 
1. [**Dialogue Query**](DialogueCondition.md#dialogue-query)
2. [**Boolean Conditions**](DialogueCondition.md#boolean-conditions)
3. [**Integer Conditions**](DialogueCondition.md#integer-conditions)
4. [**Float Conditions**](DialogueCondition.md#float-conditions)
<br>

### Dialogue Query 
The condition's dialogue query can be selected freely and determines most of its scope and behavior. Put another way, conditions exist to turn queries into useable boolean values over which to branch. 
<br>

### Boolean Conditions
Boolean conditions are the simplest dialogue conditions, and are associated with boolean queries. They ask the user to specify whether we are checking that the query returns true or false. 
<br>

### Integer Conditions 
Integer conditions are associated with queries that return an integer value. They ask the user to specify a comparison (greater, less, equal) and a value to compare the query's return value to. 
<br>

### Float Conditions 
Float conditions are associated with queries that return a floating point value. They ask the user to specify a comparsion (greater, less) and a value to compare the query's return value to. 
