---
layout: default
title: CRPG Camera Pawn
permalink: /CRGPCamera/Documentation/CRPGCameraPawn
---
**Click [here](Contents.md) to return to table of contents.** 

# CRPG Camera: CRPG Camera Pawn
**Extends: [APawn](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/APawn?application_version=5.3)**

Pawn that serves as an isometric "eye" for the player. Drives camera behavior. 

## Contents
1. [**Blueprint Callable Methods**](#1-blueprint-callable-methods)
    * [**Get Camera Mode**](#get-camera-mode)
    * [**Set Camera Mode**](#set-camera-mode)
    * [**Get Camera Target**](#get-camera-target)
    * [**Set Camera Target**](#set-camera-target)
    * [**Set Camera Target from Actor**](#set-camera-target-from-actor)
    * [**Add Move Input**](#add-move-input)
    * [**Add Rotation Input**](#add-rotation-input)
    * [**Add Zoom Input**](#add-zoom-input)
2. [**Data Attributes**](#2-data-attributes)
    * [**Zoom Sensitivity**](#zoom-sensitivity)
    * [**Rotate Sensitivity**](#rotate-sensitivity)
    * [**Default Hover Height**](#default-hover-height)
    * [**Ground Trace Channel**](#ground-trace-channel)
    * [**Reset Rotation on Follow**](#reset-rotation-on-follow)
    * [**Target Component Tag**](#target-component-tag)
3. [**Components**](#3-components)
    * [**Root Sphere**](#root-sphere)
    * [**Camera Boom**](#camera-boom)
    * [**Camera**](#camera)
    * [**Movement**](#movement)

## 1. Blueprint Callable Methods
The following methods serve as the public interface for the class and can be called via blueprint.

### Get Camera Mode
```cpp
/**
* Gets the current camera mode. 
* 
* @return ECRPGCameraMode - current mode. 
*/
ECRPGCameraMode GetCameraMode() const;
```
**Note:** See [**CameraMode**](#camera-mode) for more information. 

### Set Camera Mode
```cpp
/**
* Sets the current camera mode. 
* 
* @param InMode - the new mode. 
*/
void SetCameraMode(ECRPGCameraMode InMode);
```
**Note:** See [**CameraMode**](#camera-mode) for more information.

### Get Camera Target
```cpp
/**
* Retrieves the current camera target, whether or not it is currently being 
* followed. 
* 
* @return USceneComponent* - the target component. 
*/
USceneComponent* GetCameraTarget() const;
```

### Set Camera Target
```cpp
/**
* Sets the camera's follow target to the given component. 
* 
* @param InTarget - the component we want to track.
* @param bFollow - whether we immediately want to start following the target.
*/
void SetCameraTarget(USceneComponent* InTarget, bool bFollow);
```

### Set Camera Target From Actor 
```cpp
/**
* Sets the camera's follow target to the given actor. If the actor has a scene
* component with a matching target component tag, that will be used. Otherwise 
* the actor's root will be used. 
* 
* @param InActor - the target actor. 
* @param bFollow - whether we should start following the actor immediately. 
*/
void SetCameraTargetFromActor(AActor* InActor, bool bFollow);
```

### Add Move Input
```cpp
/**
* Adds movement input to "pan" the camera. If we are in follow mode, the camera
* will switch to free mode. 
* 
* @param InInput - the input vector (X for Right-Left, Y for Forward-Back)
*/
void AddMoveInput(FVector2D InInput);
```

### Add Rotation Input
```cpp
/**
* Adds rotation input to turn the camera from side to side. 
* 
* @param InInput - the direction/degree of rotation. 
*/
void AddRotationInput(float InInput);
```

### Add Zoom Input
```cpp
/**
* Adds zoom input to adjust the length of the camera's spring arm. 
* 
* @param Input - the direction/degree of the zoom. 
*/
void AddZoomInput(float Input);
```

## 2. Data Attributes
The following properties can be set in the pawn's details panel and allow for its functionality to be customized. 

### Zoom Sensitivity
**EditAnywhere**
* **Type:** float
* **Access:** Private
* **Description:** How much the zoom length should change when input is applied.

### Rotate Sensitivity
**EditAnywhere**
* **Type:** float
* **Access:** Private
* **Description:** How far the camera should rotate when input is applied.

### Default Hover Height
**EditAnywhere**
* **Type:** float
* **Access:** Private
* **Description:** The root component's desired height above the ground when in "free" movement mode. Think of this as the height of an invisible "virtual" character that the camera is looking at. 

### Ground Trace Channel 
**EditAnywhere**
* **Type:** ECollisionChannel
* **Access:** Private
* **Description:** The trace channel to use to detect the ground.

### Reset Rotation on Follow 
**EditAnywhere**
* **Type:** bool
* **Access:** Private
* **Description:** If true, the camera will match the rotation of its target when entering "follow" mode. If false, it will keep its current rotation. 

### Target Component Tag
**EditAnywhere**
* **Type:** FName
* **Access:** Private
* **Description:** Component tag that can be used to find the desired target component when calling SetCameraTargetFromActor(). 

### Draw Debugs
**EditAnywhere, EditorOnly**
* **Type:** bool
* **Access:** Private
* **Description:** If true, debug information will be drawn to the screen. 

### Camera Mode 
**VisibleAnywhere** //Todo: change to visible anywhere
* **Type:** ECRPGCameraMode
* **Access:** Private
* **Description:** The current movement mode for the camera. There are two options:
    1. **ECRPGCameraMode::Free:** In this movement mode, the camera hovers off the ground, moving freely when the appropriate functions are called. 
    2. **ECRPGCameraMode::Follow:** In this movement mode, the camera follows a target actor. 

## 3. Components
The following actor components are present on the pawn and can be used to further customize the camera's functionality. 

### Root Sphere
* **Type:** [**USphereComponent**](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Components/USphereComponent/__ctor?application_version=5.3)
* **Description:** Root of the pawn actor that serves as a "look" location for the camera. Collides with nothing by default, but can be set to collide with specific objects to further restrict camera movement if so desired. 

### Camera Boom 
* **Type:** [**UZoomableSpringArm**](ZoomableSpringArm.md)
* **Description:** Offsets the camera from its root component. Functions like any spring arm component, but with the added ability to zoom in and out. Modify this to adjust the way the camera zooms and tilts. 

### Camera 
* **Type:** [**UCameraComponent**](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Camera/UCameraComponent?application_version=5.3)
* **Description:** The actual camera.

### Movement
* **Type:** [**UFloatingPawnMovement**](https://dev.epicgames.com/documentation/it-it/unreal-engine/API/Runtime/Engine/GameFramework/UFloatingPawnMovement%3Fapplication_version%3D5.3)
* **Description:** Handles raw movement for the camera pawn. Here you can adjust speed, acceleration, etc. 