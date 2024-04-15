---
layout: default
title: Dialogue Speech Details Documentation
permalink: /DialogueTree/Documentation/FSpeechDetails
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: FSpeechDetails 
Struct used to pass information about an individual dialogue speech.

## Contents 
1. [**Data Attributes**](FSpeechDetails.md#1-data-attributes)
   * [**Speech Text**](FSpeechDetails.md#speech-text-blueprintreadonly)
   * [**Speaker Name**](FSpeechDetails.md#speaker-name-blueprintreadonly)
   * [**Speech Audio**](FSpeechDetails.md#speech-audio-blueprintreadonly)
   * [**Behavior Flags**](FSpeechDetails.md#behavior-flags-blueprintreadonly)
   * [**bIgnoreContent**](FSpeechDetails.md#bignorecontent-blueprintreadonly)
   * [**bCanSkip**](FSpeechDetails.md#bcanskip-blueprintreadonly)
   * [**bIsLocked**](FSpeechDetails.md#bislocked-blueprintreadonly)
   * [**OptionMessage**](FSpeechDetails.md#optionmessage-blueprintreadonly)

## 1. Data Attributes 
The following are the data attributes associated with the struct. 
<br>

### Speech Text (BlueprintReadOnly)
* **Type:** FText
* **Access:** Public
* **Description:** The text of the speech.
<br>

### Speaker Name (BlueprintReadOnly)
* **Type:** FName
* **Access:** Public
* **Description:** The name of the speaker.
<br>

### Speech Audio (BlueprintReadOnly)
* **Type:** USoundBase*
* **Access:** Public
* **Description:** The audio associated with the speech.
<br>

### Behavior Flags (BlueprintReadOnly)
* **Type:** FGameplayTagContainer
* **Access:** Public
* **Description:** Any gameplay tags serving as behavior flags associated with the speech. These are effectively tags that can be used to trigger animations, etc.
* **Note:** GameplayTagContainers and their GameplayTags might not be familiar to all users, but they are very quick to learn, very flexible and useful in a broad range of situations. 
<br>

### bIgnoreContent (BlueprintReadOnly)
* **Type:** bool
* **Access:** Public
* **Description:** Whether the speech content should be ignored when entering the node. Defaults to false.  
<br>

### bCanSkip (BlueprintReadOnly)
* **Type:** bool
* **Access:** Public
* **Description:** Whether the player is allowed to skip the speech. Defaults to true. 
<br>

### bIsLocked (BlueprintReadOnly)
* **Type:** bool 
* **Access:** Public
* **Description:** Used only on speech options. Whether the option is locked or free to be selected.
<br>

### OptionMessage (BlueprintReadOnly)
* **Type:** FText 
* **Access:** Public
* **Description:** Used only on speech options. Optional message to attach to the speech when used as an option.
<br>
