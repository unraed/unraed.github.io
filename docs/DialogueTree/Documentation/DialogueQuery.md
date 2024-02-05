---
layout: default
title: Dialogue Query Documentation
permalink: /DialogueTree/Documentation/DialogueQuery
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Dialogue Query
Dialogue Queries are used to retrieve information for use in dialogue. Generally speaking, this is information pulled from the wider world of the game, and it gets used as part of a [**Dialogue Condition**](DialogueCondition.md) to establish branching logic in dialogue. Custom queries can be created in Blueprint by extending SpeakerQueryBool (for queries that return a boolean value), SpeakerQueryInt (for queries that return an integer value), and SpeakerQueryFloat (for queries that return a double/float value). 

## Contents
1. [**Built in Queries**](DialogueQuery.md#1-built-in-queries)
   * [**Speaker Found Query**](DialogueQuery.md#speaker-found-query)
   * [**Node Visited Query**](DialogueQuery.md#node-visited-query)
2. [**Custom Queries**](DialogueQuery.md#2-custom-queries)
   * [**Query Speaker**](DialogueQuery.md#query-speaker-blueprintimplementableevent)
   * [**Is Valid Speaker Query**](DialogueQuery.md#is-valid-speaker-query-blueprintnativeevent)
   * [**Get Graph Description**](DialogueQuery.md#get-graph-description-blueprintnativeevent)

## 1. Built in Queries 
Two queries are provided pre-made. These are: 
<br>

### Speaker Found Query 
Determines if the dialogue asset has been provided with a Speaker Component for the specified speaking role. Useful for cases where the speaker may or may not be present in dialogue, as attempting to play a speech for a speaker whose component is missing will force exit the dialogue. 

* Boolean type. Returns true if the speaker component is found. False otherwise.
* Requires the user to specify the target speaker in the dialogue editor. 
<br>

### Node Visited Query 
Checks if the specified node has already been visited in dialogue. 

* Boolean type. Returns true if the target node has already been visited. Otherwise false.
* Requires the user to specify the target node in the dialogue editor.
<br>

## 2. Custom Queries 
As discussed above, custom queries are made in Blueprint by extending SpeakerQueryBool, SpeakerQueryInt or SpeakerQueryFloat, depending on the desired return type of the query. Note that custom queries must always have a Speaker Component to act upon/through. 

Like with dialogue events, any properties created should be fillable via the dialogue editor. When creating a custom query, the user must implement the following methods/events:
<br>

### Query Speaker (BlueprintImplementableEvent)
Provides the actual logic of querying the speaker. Must be overridden to create an effective Custom Query. Return value depends on the type of query being implemented. 

#### For Speaker Query Bool: 
```cpp
/**
* User specified query. Implemented via blueprint.
*
* @param InSpeaker - UDialogueSpeakerComponent*, target speaker.
* @return bool - the value of the query.
*/
bool QuerySpeaker(const UDialogueSpeakerComponent* InSpeaker) const;
```
<br>

#### For Speaker Query Int: 
```cpp
/**
* User specified query. Implemented via blueprint. 
* 
* @param InSpeaker - UDialogueSpeakerComponent*, target speaker.
* @return int32 - the value of the query. 
*/
int32 QuerySpeaker(const UDialogueSpeakerComponent* InSpeaker) const;
```
<br>

#### For Speaker Query Float:
```cpp
/**
* User specified query. Implemented via blueprint.
*
* @param InSpeaker - UDialogueSpeakerComponent*, target speaker.
* @return double - the value of the query.
*/
double QuerySpeaker(const UDialogueSpeakerComponent* InSpeaker) const;
```
<br>

### Is Valid Speaker Query (BlueprintNativeEvent)
Can be overridden to specify conditions the Query needs to satisfy in order to compile. Useful when using variables that can have a null value; allows you to require these to be filled in order to compile the dialogue. Simply returns true if not overridden.

```cpp
/**
* User defineable function to check if the query is valid. 
* 
* @return bool - True if valid according to terms user sets. False 
* otherwise.
*/
bool IsValidSpeakerQuery() const;
```
<br>

### Get Graph Description (BlueprintNativeEvent)
Retrieves the display text for the query in the dialogue editor. Failing to override this method will result in the class name being used instead. 

```cpp
/**
* Retrieves the text to display for the query in the graph editor. Should
* be implemented by the user as a blueprint native event. 
*/
FText GetGraphDescription() const;
```

