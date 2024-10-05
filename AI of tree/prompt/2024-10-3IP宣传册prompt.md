---
title: 2024-10-3IP宣传册prompt
tags: 
grammar_cjkRuby: true
---


multi-panel mood board, split into multiple boxes, [PRODUCT] mockups, including lifestyle images, product shots, color swatches, and textures, [COLOR SCHEME] palette, high contrast, [EMOTION/MOOD] branding

![enter description here](https://gitee.com/feasdada/IMGtest/raw/master/小书匠/1727974629709.png)


For anyone following along at home, here are some steps I jotted down whilst I was in the thick of it.

Research anatomy via Google and whatever resources you have available. Identify the function of each and every superficial muscle, as well as the not-so-superficial ones that have an effect on the superficial ones. Identify the origin and insertion of each muscle, and try to wrap your head around how the muscle actions affect their shape.
Model all the superficial muscles based on the above, using a bare minimum of geometry.
Model the bony landmarks as a separate object.
Parent the muscle and bone objects to the main skeleton armature.
Add helper bones that are driven by the rotations of the main armature, and weight portions of the muscles to them. Try and get it most of the way with the weights first, then add corrective shape keys.
For bigger, longer muscles like the biceps and triceps, make a bone the same length as the muscle, with a smaller bone at its end, and add a Stretch To constraint. Target the long bone to the end one, and weight the muscle to the long bone. Now you can make use of the Volume Variation parameter to make the muscle flex
Add two Shrinkwrap modifiers and two Smooth modifiers to the skin object. Set one of each to target the bones object, and the other two to target the muscles. The modifiers targeting the bones object should be positioned above the muscles ones. This allows the muscles to slide over the bones to some degree.
Make an animation of the fingers, wrist and arm covering their full range of motion, and reshape every muscle and tweak every helper bone so that they conform as closely as possible to the shape of the skin base mesh throughout the animation. Wherever it slips out of position, adjust the weights, make corrective shape keys or add drivers to the helper bones.
Make shape keys for the muscles and bones so they correspond to genders, races and other general body shape keys, and adjust everything to make sure each one of those also stays aligned throughout the range of motion animation without disrupting each other or anything else.
After going mad trying to eradicate all the knots in the skin caused by the tangled mess of muscles all passing through each other, merge the muscles together where possible to help keep them in alignment.
Fix the shape of the muscles subsequent to the merging, and redo all their shape keys, weights and helpers again so they once again conform to all the animation poses, genders etc.
Go through this process several more times without pulling your hair out.
Realise that you forgot to account for proportion controls, and proceed to reshape every muscle to fit the scaling of every finger, arm, neck etc. and then go and adjust the corrective shapes to fit every pose.
Reshape all the muscles to fit all the shape keys in all the poses all over again every time you touch something or look at it the wrong way.
Check yourself into a mental institution (optional).