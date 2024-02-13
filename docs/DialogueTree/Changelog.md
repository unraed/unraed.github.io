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