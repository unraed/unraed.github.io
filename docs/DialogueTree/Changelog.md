---
layout: default
title: Dialogue Tree Changelog
permalink: /DialogueTree/Changelog
---
**Click [here](DialogueTree.md) to return to the Dialogue Tree home page.** 

# Dialogue Tree: Changelog
Below you will find a brief summary of changes made to the plugin. 

## Initial Release - v1.0  
- Plugin released on the Unreal Marketplace 

## 2/12/2024 - v1.0, Hotfix 1 
- Fixed an issue that was causing node visuals not to load in the plugin build downloaded from the Unreal Marketplace. 

## 2/13/2024 - v1.0, Hotfix 2
- Adjusted the zOrder of the template widgets in the viewport to account for conflicts with other widgets/plugins that may accidentally make a Canvas Panel visible, thereby blocking the dialogue widget from receiving input. Dialogue Menu Widgets should now spawn "above" any blocking widgets. 

## Coming Soon - v1.0, Hotfix 3
- Modified the default Dialogue Controller, adding several public properties to customize widget and input behavior. These properties can be found on the Dialogue Controller actor under the "Dialogue" category. 
    * Mouse cursor visibility is now cached when entering dialogue, and restored on leaving it. 
    * ZOrder for the dialogue widget in the viewport is now a customizable property. 
    * A new "Default Input Mode" struct allows users to customize the input mode the game reverts to on closing dialogue. 
    * New "Allow Game Input in Dialogue" boolean property allows users to customize whether the system changes the input mode to UI Only or Game and UI on starting dialogue. Default behavior has been changed to UI Only, which is a departure from prior builds. 

For more information see the documentation page for the Dialogue Controller [**here**](Documentation/DialogueController.md).