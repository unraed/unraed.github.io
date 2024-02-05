---
layout: default
title: Dialogue Speaker Socket Documentation
permalink: /DialogueTree/Documentation/DialogueSpeakerSockett
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Dialogue Speaker Socket
**Extends: [UObject](https://docs.unrealengine.com/5.1/en-US/API/Runtime/CoreUObject/UObject/UObject/)**

Proxy object that allows a speaking role to be referred to without knowing the actual Speaker Component that will fill that role. 

Users will only need to interact with the Speaker Socket via blueprint, and then only to retrieve data. For example, the speaker socket can be accessed from Dialogue Events and Speaker Queries to retrieve the name of the target speaking role. 

## Contents
1. [**Data Attributes**](DialogueSpeakerSocket.md#1-data-attributes)
- [**Speaker Name**](DialogueSpeakerSocket.md#speakername)
2. [**Blueprint Callable Methods**](DialogueSpeakerSocket.md#2-blueprint-callable-methods)
- [**Get Speaker Name**](DialogueSpeakerSocket.md#get-speaker-name-blueprintcallable)

## 1. Data Attributes
The following are data attributes associated with the class. 
<br>

### SpeakerName
* **Type:** FName
* **Access:** Private
* **Description:** The name of the target speaking role. 

## 2. Blueprint Callable Methods
The following methods can be called, but not overridden, via blueprint. 
<br>

### Get Speaker Name (BlueprintCallable)
```cpp
/**
* Retrieves the speaker's name. 
* 
* @return FName, the speaker's name
*/
FName GetSpeakerName() const;
```
