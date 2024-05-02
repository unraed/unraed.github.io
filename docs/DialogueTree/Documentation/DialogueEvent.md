---
layout: default
title: Dialogue Event Documentation
permalink: /DialogueTree/Documentation/DialogueEvent
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Dialogue Event
Dialogue events can be used to trigger an effect from dialogue on the wider world of your game. A new event can be created via Blueprint by extending UDialogueEvent. 

## Contents 
1. [**Built in Events**](DialogueEvent.md#1-built-in-events)
   * [**Reset Node Visits**](DialogueEvent.md#reset-node-visits)
   * [**Reset all Node Visits**](DialogueEvent.md#reset-all-node-visits)
   * [**Set Resume Node**](DialogueEvent.md#set-resume-node)
   * [**DTE_LogToScreen**](DialogueEvent.md#dte_logtoscreen)
2. [**Data Attributes**](DialogueEvent.md#2-data-attributes)
   * [**Speaker**](DialogueEvent.md#speaker-editanywhere)
3. [**Editing Event Properties From Dialogue**](DialogueEvent.md#3-editing-event-properties-from-dialogue)
4. [**Blueprint Implementable Methods**](DialogueEvent.md#4-blueprint-implementable-methods)
   * [**On Play Event**](DialogueEvent.md#on-play-event-blueprintnativeevent)
   * [**Is Valid Event**](DialogueEvent.md#is-valid-event-blueprintnativeevent)
   * [**Get Graph Description**](DialogueEvent.md#get-graph-description-blueprintnativeevent)
5. [**Helper Functions**](DialogueEvent.md#helper-functions)
   * [**Get Speaker Socket**](DialogueEvent.md#get-speaker-socket-blueprintcallable)
   * [**Get Additional Speaker Sockets**](DialogueEvent.md#get-additional-speaker-sockets-blueprintcallable)
  
## 1. Built in Events
Three Events are included with the plugin. These are:
<br>

#### Reset Node Visits
Marks the specified node unvisited. Requires the user to stipulate the target node in the details panel. 
<br>

#### Reset All Node Visits
Marks all nodes in the dialogue unvisited, effectively resetting it to an unplayed state. 
<br>

#### Set Resume Node
Sets the node for the current dialogue to resume from when starting dialogue with "bResume" set to true. 
<br>

#### DTE_LogToScreen
For debugging. The equivalent of Blueprint's PrintString() function (literally calls it). Allows the user to specify a message to log to the screen. Only works in development builds. 
<br>


## 2. Data Attributes 
All dialogue events share the following data attributes. 
<br>

### Speaker (EditAnywhere)
* **Type:** UDialogueSpeakerSocket* 
* **Access::** Protected
* **Description:** All dialogue events require a speaker to operate on/through. The speaker is not directly accessible via Blueprint (it is not BlueprintReadWrite for example). It must be filled via the dialogue editor and can be interacted with via overrideable methods. See below. 
<br>

## 3. Editing Event Properties From Dialogue 
Variables you create as part of your events are editable from the dialogue graph in the details panel. Please note that all the normal rules apply just the same as if you were working in Blueprint. Namely, if you rely on a non-primitive object reference and then forget to fill it in the dialogue editor you **will** encounter bugs. When using such variables, overriding IsValidEvent() can help protect you from bad data. See below. 

## 4. Blueprint Implementable Methods 
The following methods/events should be overridden as part of your custom dialogue event.
<br>

### On Play Event (BlueprintNativeEvent)
Contains the actual logic of your event. Override this method to specify the event behavior. Otherwise it won't do anything. 

```cpp
/**
* User specified behavior for the event.
* 
* @param InSpeaker - FSpeakerActor, struct containing target speaker component and actor
* @param OtherSpeakers - TArray<FSpeakerActor>, any additional speakers
* component to operate on. 
*/
void OnPlayEvent(FSpeakerActorEntry InSpeaker, const TArray<FSpeakerActorEntry>& OtherSpeakers);
```
<br>

### Is Valid Event (BlueprintNativeEvent)
Can be overridden to specify conditions the Event needs to satisfy in order to compile. Useful when using variables that can have a null value; allows you to require these to be filled in order to compile the dialogue. Simply returns true if not overridden. 

```cpp
/**
* Checks if the event is valid and has all of the information it needs 
* to compile. Should be user defined to ensure that all events take their
* custom fields into account. 
* 
* @return bool - True if all requisite data is present; false otherwise.
*/
bool IsValidEvent() const;
```
<br>

### Get Graph Description (BlueprintNativeEvent)
Gets the text to display in the dialogue editor for this event. If you do not override this event, the editor will use the Event's class name. See the [**Queries and Events**](../Tutorials/QueriesAndEvents.md) tutorial for more information. 

```cpp
/**
* Gets the graph description text for the event. User defined to allow
* for custom descriptions. 
*/
FText GetGraphDescription() const;
```

### Helper Functions 
The following functions are useful helpers when working with events.

#### Get Speaker Socket (BlueprintCallable)
Retrieves the primary target speaker socket for the event.

```cpp
/**
* Fetches the dialogue event's speaker socket.
*
* @return UDialogueSpeakerSocket* - the socket.
*/
UDialogueSpeakerSocket* GetSpeakerSocket() const;
```
<br>

#### Get Additional Speaker Sockets (BlueprintCallable)

Retrieves any additional target speakers supplied for the event. 

```cpp
/**
* Retrieves the list of optional additional speaker sockets for the event.
*
* @return TArray<UDialogueSpeakerSocket*> - the list of optional additional
* speakers.
*/
TArray<UDialogueSpeakerSocket*> GetAdditionalSpeakerSockets() const;
```
<br>