---
layout: default
title: Dialogue Event Documentation
permalink: /DialogueTree/Documentation/DialogueEvent
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Dialogue Event
Dialogue events can be used to trigger an effect from dialogue on the wider world of your game. A new event can be created via Blueprint by extending UDialogueEvent. 

Note: As of update 1.20, dialogue events can: 
1) be called from speeches. 
2) initiate a blocking state where the dialogue waits to proceed until the event releases it to continue.

## Contents 
1. [**Built in Events**](DialogueEvent.md#1-built-in-events)
   * [**Reset Node Visits**](DialogueEvent.md#reset-node-visits)
   * [**Reset all Node Visits**](DialogueEvent.md#reset-all-node-visits)
   * [**Set Resume Node**](DialogueEvent.md#set-resume-node)
   * [**DLGE_LogToScreen**](DialogueEvent.md#dlge_logtoscreen)
   * [**DLGE_PlayLevelSequence**](DialogueEvent.md#dlge_playlevelsequence)
2. [**Data Attributes**](DialogueEvent.md#2-data-attributes)
   * [**Speaker**](DialogueEvent.md#speaker-editanywhere)
3. [**Editing Event Properties From Dialogue**](DialogueEvent.md#3-editing-event-properties-from-dialogue)
4. [**Blueprint Implementable Methods**](DialogueEvent.md#4-blueprint-implementable-methods)
   * [**On Play Event**](DialogueEvent.md#on-play-event-blueprintnativeevent)
   * [**Is Valid Event**](DialogueEvent.md#is-valid-event-blueprintnativeevent)
   * [**Get Graph Description**](DialogueEvent.md#get-graph-description-blueprintnativeevent)
   * [**On Skipped**](DialogueEvent.md#on-skipped-blueprintnativeevent)
5. [**Blueprint Callable Methods**](DialogueEvent.md#blueprint-callable-methods)
   * [**Get Speaker Socket**](DialogueEvent.md#get-speaker-socket-blueprintcallable)
   * [**Get Additional Speaker Sockets**](DialogueEvent.md#get-additional-speaker-sockets-blueprintcallable)
   * [**Get Is Blocking**](DialogueEvent.md#get-is-blocking-blueprintcallable)
   * [**Start Blocking**](DialogueEvent.md#start-blocking-blueprintcallable)
   * [**Stop Blocking**](DialogueEvent.md#stop-blocking-blueprintcallable)
   * [**Spawn Actor to Current World**](DialogueEvent.md#spawn-actor-to-current-world-blueprintcallable)
   * [**Get Current Speech Details**](DialogueEvent.md#get-current-speech-details-blueprintcallable)
  
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

#### DLGE_LogToScreen
For debugging. The equivalent of Blueprint's PrintString() function (literally calls it). Allows the user to specify a message to log to the screen. Only works in development builds. 
<br>

#### DLGE_PlayLevelSequence
Spawns and plays a cinematic/level sequence from start to finish. Some notes about its behavior:
- Blocks until the level sequence is finished unless skipped. 
- Removes the level sequence actor from the level when finished playing (as opposed to leaving it cluttering up the level). 
- Attempts to bind the provided speaker and any additional speakers into the level sequence using their "Dialogue Name" properties as the binding tag. This can be safely ignored if no binding is desired.
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
<br>

### On Skipped (BlueprintNativeEvent)

User specified behavior for when a speech the event is attached to gets skipped in dialogue. Useful in circumstances where the event is blocking, but you want it to end immediately when Skip() is called on the speech. 

Example: The event for playing a cinematic has an OnSkipped() implementation that first sets the level sequence's play time to the end and then stops blocking so the speech can proceed. 

```cpp
/**
* User specified behavior for when a speech the event is attached
* to gets skipped.
*/
void OnSkipped();
```

### Blueprint Callable Methods
The following functions are useful methods that can be used as part of your custom events.

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

#### Get Is Blocking (BlueprintCallable)

Checks if the event is currently trying to block. In other words, checks if the event is in progress and wants dialogue to wait for it to finish before proceeding. 

```cpp
/**
* Checks if the event is currently trying to block/in progress. 
* 
* @return bool - True if blocking, False otherwise. 
*/
bool GetIsBlocking() const;
```
<br>

#### Start Blocking (BlueprintCallable)

Tells the event to start blocking. Where possible, the dialogue will then wait for the event to finish and call StopBlocking() before proceeding. 

```cpp
/**
* Sets the blocking status of the event to true. Where possible, the 
* dialogue will attempt to wait until the event completes. StopBlocking() 
* should be called to free up the dialogue to continue. 
*/
void StartBlocking();
```
<br>

#### Stop Blocking (BlueprintCallable)

Tells the event to stop blocking, thereby releasing the dialogue to proceed. 

```cpp
/**
* Marks the event as complete/frees up the dialogue to continue. Only 
* needs to be called if StartBlocking() has been called first. 
*/
void StopBlocking();
```
<br>

#### Spawn Actor to Current World (BlueprintCallable)

Spawns an actor to the currently active world. Dialogue Event's version of SpawnActorOfClass() and identical to that function in virtually every relevant way.

```cpp
/**
* Helper function to spawn an actor to the currently active
* world via a dialogue event.
*
* @param ActorClass - TSubclassOf<AActor>, the actor type to
* spawn.
* @param Location - const FVector, the location at which to
* spawn the actor.
* @param Rotation - const FRotator, the rotation at which to
* spawn the actor.
* @param SpawnParams - const FActorSpawnParameters, any
* additional spawn parameters.
* @param Owner - AActor*, actor to set as the spawned actor's 
* owner.
* @param CollisionHandlingMethod - 
* ESpawnActorCollisionHandlingMethod, how to handle collisions.
* @return AActor* - the spawned actor, or nullptr if failed to
* spawn.
*/
UFUNCTION(BlueprintCallable, Category = "DialogueEvent")
AActor* SpawnActorToCurrentWorld(TSubclassOf<AActor> ActorClass,
	const FVector Location, const FRotator Rotation, 
	AActor* Owner = nullptr, 
	ESpawnActorCollisionHandlingMethod CollisionHandlingMethod);
```
<br>

#### Get Current Speech Details (BlueprintCallable)

Helper function to get the current details of any speech the event was called from. If called from an event node, the speech details will be blank.

```cpp
/**
* Retrieves the speech details for the speech this event was 
* called from. If not called from a speech, retrieves an empty 
* speech details struct.
* 
* @param InDetails - FSpeechDetails, the new speech details. 
*/
const FSpeechDetails GetCurrentSpeechDetails() const;
```