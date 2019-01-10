---
layout: post
title:  "Inner Shadows and Script Updates"
author: line0
---

It's been a while since my last blog post and writing another huge one has proven to be a daunting task, so I decided to switch gears and go for shorter yet more frequent updates instead.

## Creating an Inner Shadow

Today we are going typeset a sign that requires us to add an inner shadow, which is an issue when you have to do it using only Aegisub but takes only a few steps when be done in Illustrator. This tutorial assumes you have a recent version of Aegisub, Illustrator and AI2ASS installed and you're familiar with using these tools (If you're not, read here first). Let's cut to the chase...

1. ... and load our sign into AI: [![Inner Shadow Sample: SoreMachi "Oya Highschool"](/assets/img/2015/01/Soredemo-Machi-wa-Mawatte-Iru-Ep02_001_173-580x326.png)](/assets/img/2015/01/Soredemo-Machi-wa-Mawatte-Iru-Ep02_001_173.png)
2. Pick an appropriate font (I chose Iwata Mincho Bold) and add a new text layer with the sign translation "Oya Highschool". Place it somewhere above the original size, but don't concern yourself with the rotation or gradient - we are going to apply these in Aegisub. [![oya_1](/assets/img/2015/01/oya_1-580x272.png)](/assets/img/2015/01/oya_1.png)
3. Expand the the text to outlines and create a duplicate we are going to use as the inner shadow. Lock and hide the original fill layer.
4. Draw a filled rectangle over the text, select both (or everything if all other layers are locked) and use the ![Adobe Illustrator: Exclude Pathfinder](/assets/img/2015/01/pf_exclude.png) _Exclude Pathfinder_ to create a cutout shape. Turn the whole shape into a _Compound Path._[![oya_3](/assets/img/2015/01/oya_3-580x333.png)](/assets/img/2015/01/oya_3.png)
5. Add the Effect > Stylize > Drop Shadow_ Layer Style. In the _Drop Shadow Dialog_ set _Opacity_ to 100%, _Blur_ to 0pt and pick a color that allows you to judge the amount of _X_ and _Y Offset_ required to match the original sign. [![oya_4](/assets/img/2015/01/oya_4-580x438.png)](/assets/img/2015/01/oya_4.png)
6. When you're done, click Object > Expand Appearance and use the ![Adobe Illustrator: Minus Front Pathfinder](/assets/img/2015/01/pf_minusfront.png)Minus Front Pathfinder to get only the inner shadow outlines. Delete the drop shadow of the rectangle, re-enable the fill layer and check your result. [![oya_5](/assets/img/2015/01/oya_5-580x289.png)](/assets/img/2015/01/oya_5.png)
7. For the bright highlight you have 2 options:
  A. Create another copy of the fill layer, add a drop shadow, expand the result and use the ![Adobe Illustrator: Unite Pathfinder](/assets/img/2015/01/pf_unite.png)_Unite Pathfinder_ to get a composite shape we can use as the bottom layer in our ASS script.
  B. Create a duplicate of the fill layer with a position offset in Aegisub and use that as the bottom layer.
8. Export your sign using AI2ASS and apply gradients and rotation in Aegisub. Done. [![Final Sign](/assets/img/2015/01/Soredemo-Machi-wa-Mawatte-Iru-Ep02_003_173-580x326.png)](/assets/img/2015/01/Soredemo-Machi-wa-Mawatte-Iru-Ep02_003_173.png)

## Automation Script News

Perhaps this is a good time to plug one of my new scripts and a few improvements in other scripts you shouldn't miss out on. First of all, lyger's [Gradient Everything](https://github.com/lyger/Aegisub_automation_scripts/blob/master/gradient-everything.lua "Gradient Everything") got an [update](https://github.com/lyger/Aegisub_automation_scripts/pull/3) that makes use of [ASSInspector](https://github.com/TypesettingTools/ASSInspector "ASSInspector") to determine the bounding box for the gradient strips, so you no longer have to draw a clip manually. I also added a new [AI2ASS](https://github.com/torque/AI2ASS "AI2ASS") export mode that creates full ASS dialogue lines which contain, among other values, the numbers and names of your Illustrator layers. [Paste AI Lines](https://github.com/TypesettingTools/line0-Aegisub-Scripts/blob/master/PasteAILines.lua) is a companion macro for convenient pasting of _AI2ASS_ exported lines into Aegisub. Features include:

* **Trim Drawings:** makes drawings start at the top left point of their bounding box instead of at the script coordinate origin. This makes the dragging point appear next to the drawings (or inside depending on the chosen alignment) instead of at the top left on the the preview window, which in turn allows for easier dragging and rotation without having set an origin.
* **Layer Offset:** provides a few ways of adjusting the AI layer numbers to your ASS script.
  1. **Auto Mode:** the layer number of each imported lines is offset in a way that makes them appear above all the currently selected lines, but without any number gap between the highest selected layer and lowest imported layer. This is the Default and should fit quite well into common workflows.
  2. **Unique Mode:** the layer number is incremented for every imported line starting at [highest selected layer + 1]. Use this mode if the stacking order of object inside your AI layers matters.
  3. **Offset Mode:** takes the layer numbers from your AI document and adds the configurable value. The offset value can also be used as an additional offset for the other 2 modes.
* **Copy Times:** copies the cumulative start and end times of the selected lines.
* **Set Style**: the style name of _AI2ASS_ lines is hardcoded to 'AI'. If you want to use a different style, enter it here.
* **Remove Actor**: use this if you don't want the layer name appear in the actor field.

The script requires a bunch of modules: [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) (which also got an update), [ASSFoundation](https://github.com/TypesettingTools/ASSFoundation) and by extension _ASSInspector_. Another macro that may prove useful to many of you is my script cleaner [ASSWipe](https://github.com/TypesettingTools/line0-Aegisub-Scripts/blob/master/ASSWipe.lua) (trying to follow in torque's footsteps wrt terrible ASS puns here). It removes duplicate, redundant or otherwise ineffective override tags and junk from your lines, filters useless clips, deletes invisible lines and combines identical lines so long as they are consecutive in time (e.g. created by line2fbf script). It shares all of its requirements with _Paste AI Lines__,_ and to avoid confusion I'm currently distributing [test snapshots](//files.line0.eu/builds/ASSWipe/) that contain up-to-date versions of all required modules. I'm always open for questions, suggestions and bug reports concerning my tools and tutorials. You may use the comment section, but as this blog has very few readers i tend to only check it sporadically, so I'd suggest you contact me via IRC or create a Github issue if you want a swift reply. For general typesetting questions **not covered in the available guides**, I invite you (yes, all 3 of you!) to join #irrational-typesetting-wizardry on Rizon, where you can meet pretty much all of the relevant TSers in (English speaking) fansubbing .