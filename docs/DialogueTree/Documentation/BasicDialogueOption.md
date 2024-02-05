---
layout: default
title: Basic Dialogue Option Widget Documentation
permalink: /DialogueTree/Documentation/BasicDialogueOption
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Basic Dialogue Option

Widget used by the [**Basic Dialogue Display**](DialogueDisplayWidget.md#basic-dialogue-display) and the [**CRPG Dialogue Display**](DialogueDisplayWidget.md#crpg-dialogue-display) to represent a selectable option. Fairly simple, but with a couple of customizable elements worth discussing.

## Contents 
1. [**Widget Details**](BasicDialogueOption.md#1-widget-details)
   * [**Bullet Point**](BasicDialogueOption.md#bullet-point)
   * [**Button Appearance and Audio**](BasicDialogueOption.md#button-appearance-and-audio)

## 1. Widget Details
While the whole widget is adjustable in UMG, the following elements ought to be called out 
explicitly, as most users will likely want to customize them and they can be a little hidden. 

### Bullet Point 
This is the little tick mark that appears in front of dialogue options. You can supply your own 2D texture under the "Brush" category. 

### Button Appearance and Audio
This is where you can adjust the appearance of the option button as a whole. 

Without digging into UMG buttons too much, you can adjust the normal, hovered, and pressed appearance of the button independently under the "Style" category. 

You can also change the sound that plays when clicking the button under "Style">>"Pressed Sound". This in particular can be a little hard to track down if you don't know where to look, so I wanted to call it out specifically. 
