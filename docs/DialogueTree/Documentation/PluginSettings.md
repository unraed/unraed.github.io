---
layout: default
title: Dialogue Tree Plugin Settings Documentation
permalink: /DialogueTree/Documentation/PluginSettings
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Plugin Settings
The plugin settings can be found under ProjectSettings>>Dialogue Tree and offer a number of handy properties for configuring the plugin in your project. 

## Contents
1. [**Dialogue Controller Type**](PluginSettings.md#dialogue-controller-type)
2. [**Default Dialogue Controller Settings**](PluginSettings.md#default-dialogue-controller-settings)
    * [**Widget Type**](PluginSettings.md#dialogue-widget-type)
    * [**Widget ZOrder**](PluginSettings.md#widget-zorder)
    * [**Default Input Mode**](PluginSettings.md#default-input-mode)
    * [**Allow Game Input in Dialogue**](PluginSettings.md#allow-game-input-in-dialogue)

## Dialogue Controller Type
This option allows you to select any class inheriting from ADialogueController to serve as the controller for your dialogues. The system will spawn in a single controller of the specified type, sharing the lifespan of your world. 

By default, the system will use the provided BP_BasicDialogueController class. 

## Default Dialogue Controller Settings
The following settings apply specifically to the default BP_BasicDialogueController, which uses them as configuration options. 

### Dialogue Widget Type 
The type of dialogue display widget that the controller will use to present dialogue to the user. Only valid widgets, implementing BI_SimpleDialogueDisplay will be selectable. 

If none is supplied here, the controller will use W_BasicDialogueDisplay. 

### Dialogue Option Widget Type
The type of dialogue option widget that will be used to allow the player to pick options in dialogue. Only valid widgets, implementing BI_SimpleDialogueOption will be selectable. 

If none is supplied here, the controller will use W_BasicDialogueOption. 

### Widget ZOrder
Some users have found a conflict between the provided dialogue display widgets and their existing widgets. What is happening there is that their existing widgets have a canvas panel for a root. When the existing widget is set to "visible" using a function, the canvas panel becomes hit-testable. If it is situated above the dialogue widget in the viewport it winds up consuming mouse input before the input ever reaches the dialogue widget. 

As a workaround, the default dialogue controller now has a configurable ZOrder property to control what position its widgets will use in the viewport. This is already set quite high to avoid such conflicts, but if you encounter an issue where you cannot interact with the widget you may want to try boosting the ZOrder further. 

### Default Input Mode
This struct allows you to configure the input mode that the system will return to on exiting dialogue. Unfortunately there does not seem to be a way of retrieving the current input mode, and so there is no way to do this automatically via caching. This setting is the admittedly somewhat awkward workaround. It's settings include: 
    * **Input Mode:** This is an enum representing the possible input modes that you can select. As such it is the most important setting here. Options include Game Only(default), Game and UI, and UI Only. 
    * **Flush Input:** This is a boolean toggle to determine if we flush input on changing the mode. In general, I would recommend leaving this on. 
    * **Hide Cursor During Capture:** Whether the cursor should be hidden during capture. This will only apply for Game and UI mode. 
    * **Mouse Lock Mode:** This allows you to determine the lock mode for the mouse on changing the input mode. It is not used for the Game Only input mode. 

### Allow Game Input in Dialogue
This is a boolean toggle to determine the input mode when navigating dialogue. 

If set to "True," the system will use the "Game and UI" input mode. This allows the player character to continue to consume input alongside the dialogue menu (like Skyrim, where you can walk away from someone you're talking to). 

The default value of "False" will use "UI Only" as an input mode. This will prevent all normal game input, effectively rooting the character and camera in place while dialogue is ongoing. 
