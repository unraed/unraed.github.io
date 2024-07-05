---
layout: default
title: Zoomable Spring Arm
permalink: /CRGPCamera/Documentation/ZoomableSpringArm
---
**Click [here](Contents.md) to return to table of contents.** 

# CRPG Camera: Zoomable Spring Arm
**Extends: [USpringArmComponent](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/USpringArmComponent?application_version=5.3)**

A spring arm component that can smoothly change its arm length to "zoom" in and out. Allows different zoom strategies.

## Contents
1. [**Blueprint Callable Methods**](#1-blueprint-callable-methods)
    * [**Zoom to Arm Length**](#zoom-to-arm-length)
2. [**Data Attributes**](#2-data-attributes)
    * [**Zoom Strategy Type**](#zoom-strategy-type)
    * [**Interp Speed**](#interp-speed)
    * [**Max Arm Length**](#max-arm-length)
    * [**Min Arm Length**](#min-arm-length)
    * [**Tilt Curve**](#tilt-curve) 

## 1. Blueprint Callable Methods
The following methods serve as the public interface for the class and can be called via blueprint. 

### Zoom to Arm Length
```cpp
/**
* Tells the zoomable spring arm component to smoothly zoom its arm length to 
* the given length. 
* 
* @param InLength - the new length. 
*/
void ZoomToArmLength(float InLength);
```

## 2. Data Attributes
The following properties can be set in the component's details panel and allow for its functionality to be customized. 

### Zoom Strategy Type 
**EditAnywhere**
* **Type:** TSubclassOf\<UZoomableSpringArmStrategy\>
* **Access:** Private
* **Description:** The type of zoom animation to apply when zooming. There are three available strategies:
    1. **Natural:** The default. Smoothly interpolates using a natural arc - eases in and out.
    2. **Constant:** Interpolates linearly/using a constant speed.
    3. **Instant:** Warps to the new zoom length. Essentially restores the default spring arm behavior.

### Interp Speed
**EditAnywhere**
* **Type:** float
* **Access:** Private
* **Description:** The speed of interpolation while zooming.

### Max Arm Length 
**EditAnywhere**
* **Type:** float
* **Access:** Private
* **Description:** The maximum allowed arm length while zooming.

### Min Arm Length
**EditAnywhere**
* **Type:** float
* **Access:** Private
* **Description:** The minimum allowed arm length while zooming.

### Tilt Curve
**EditAnywhere**
* **Type:** UCurveFloat*
* **Access:** Private
* **Description:** Curve that defines the tilt angle of the spring arm's pitch while zooming. The x-axis of the curve represents the zoom length scaled from 0.0 to 1.0. The y-axis of the curve represents the pitch angle in degrees. If not supplied, no tilt will be applied while zooming. 