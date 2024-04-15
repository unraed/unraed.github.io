---
layout: default
title: Dialogue Tree Minimum Play Time
permalink: /DialogueTree/Tutorials/OptionLockNodes
---
**Click [here](Contents.md) to return to the list of tutorials for Dialogue Tree.** 

# Dialogue Tree: Feature Update #2, Option Lock Nodes

## Help & Support
You can reach me for questions and support at unraedgames@gmail.com, or on the plugin's [**Discord Channel**](https://discord.gg/mf7mGXbePB). Feel free to reach out with any questions or requests. 

If you're enjoying the plugin, I would be extremely grateful if you could take a few moments out of your day to leave me a review on the [**Unreal Marketplace**](https://www.unrealengine.com/marketplace/en-US/product/dialogue-tree). 

If you would like to support further development on the project you can do so on [**Patreon.com**](https://www.patreon.com/UnraedGames). 

## Contents
1. [**Introduction**](OptionLockNodeTutorial.md#introduction)
2. [**How it Works**](OptionLockNodeTutorial.md#how-it-works)
3. [**Conclusion**](OptionLockNodeTutorial.md#conclusion)

## Introduction 
This is a very brief tutorial for the a new node type that is being added to the plugin in version 1.2: the Option Lock Node. 

## How it Works
Option Lock Nodes give you the ability to more easily gate certain dialogue options behind conditions. They effectively serve as a filter between a Speech Node with an Input Transition, which expects the player to select an option, and one of the options you want the player to be able to select. 

If the Lock Node's conditions evaluate to true, its child option will display and be selectable as normal. 

If the Lock Node's conditions evalutate to false, its child option will display but not be selectable. When using the default controller and widgets it will also be greyed out. 

Moreover, the Lock Node allows you to attach separate messages for when the option is locked or unlocked. For example, you might see an option displayed as: "Mais, je suis Unraed! [You don't speak French]" 

Finally, it is worth noting that Lock Nodes only have an effect when they follow a Speech Node with an Input Transition. If transitioned to under any other circumstances, the Lock Node will simply pass control on to its child node. 

## Conclusion
Just to summarize, Option Lock Nodes offer a convenient way to display certain speech options to the player while restricting whether those options can be selected. 

If you have any questions or feedback, I'd love to hear from you on my [**discord channel**](https://discord.gg/mf7mGXbePB). And if you're enjoying the plugin, I would be beyond grateful if you could take a few seconds out of your day to leave me a review on the [**Unreal Marketplace**](https://www.unrealengine.com/marketplace/en-US/product/dialogue-tree). 

Finally, if you want to support further development on the project, you can do so on [**Patreon.com**](https://www.patreon.com/UnraedGames). 

In the meantime, thanks for reading this tutorial. Good luck and happy developing.