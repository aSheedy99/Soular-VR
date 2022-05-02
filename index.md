# What Is Soular VR?
### A Project Portfolio by Finn H Tanner

<p align="center">
  <img src="docs/assets/SoularVRBlankPlanet.png?raw=true" alt="An empty, white, planet-like object hovers in mid-air. A ring-shaped table holds different coloured paints on the right, with the label 'Palette', and on the right, multiple buttons with the label 'Models'"/>
</p>

Soular VR is an creative environment built for Meta Quest 2 that allows players to shape entire worlds with their own hands! The project was inspired by creative sandbox games like <i> Minecraft </i> ,  <i> Spore </i> and <i> the Sims </i> . This page will explore my contribution as a Techincal Developer to the project, formatted in a chronological order and ending with a short reflection. Soular was made as the final project for Goldsmith's MSc XR course. As well as myself, the piece was created by Seonjeong Park (Technical), Ebba Liepe (Art) and Nicalia ThompSon (Art). Soular was built in Unity using Meta's OVR Plugin.

&nbsp;
## Technical Overview

### Player Gestures

My main task for this project was creating a flexible and performant system capable of recording hand gestures as recognisable inputs using Meta's OVR Plugin for Unity. The following code is essentially the final function used for this (although it has been simplified for ease of reading):

<details>
  <summary>Show Code</summary>
  
    [View full image.](https://github.com/aSheedy99/SoularVRProject/blob/edd58203dab4c2b792333ce69a9c67d0a293f9c1/docs/assets/PlayerGestureCarbonSnippet.png)
  
<p align="center">
  <img src="docs/assets/PlayerGestureCarbonSnippet.png">
</p>
  
</details>

&nbsp;
### Saving

<p align="center">
  <img src="docs/assets/SaveButton.png?raw=true" alt="A green button on a white table. The button has a 'book mark' logo on it. Above it in white text a label reads 'Save'"/>
</p>

A major feature we wanted to include in Soular was the ability for players to save and reload planets at a later time. I explored many methods of saving in Unity, and settled on Binary Formatting. I found this to be the most adaptable method with the only slight snag being any saved data had to be made of specific basic data types, which required at-runtime conversion of things into arrays of floats or integers.

The more complex part of this was telling the save data what object was being saved, since Game Objects werent something that could be formatted into binary. To solve this, each model is given an ID integer which correlates to a 'master list' of all models. When it comes to saving, only this integer, a position, rotation and colour are saved for each placed model. When the planet is loaded, the list is looped through, instantiating an instance of a prefab from the master list at the index specified, at the position and rotation specified etc. This increases the workload for creating models slightly, since they have to be added to the master list and given the appropriate ID, but makes it very quick and easy to save and load.

&nbsp;
### Painting

A main feature of Soular is the ability to paint the planet surface in different colours. For this, I created a vertex-colour shader that works with a 'paint brush' the player can use. When the brush collides with the planet, the colour of the vertices of the nearest chunk are changed to the chosen colour. We used a chunk system to limit how many vertices were check through to improve performance, since each one had a square distance check. The code below is a simplee foreach loop that demonstrates a simplified version of how this works.

<details>
  <summary>Show Code</summary>
  
    [View full image.](https://github.com/aSheedy99/SoularVRProject/blob/edd58203dab4c2b792333ce69a9c67d0a293f9c1/docs/assets/VertexColourCarbonSnippet.png)
  
<p align="center">
  <img src="docs/assets/VertexColourCarbonSnippet.png">
</p>
  
</details>

&nbsp;
### Menu and UI

Whilst the artist side of the UI fell to other team members, it was my role to develop much of the functional side of the physical UI. I handled interactions by spawning sphere triggers on the finger tips of each hand, allowing me to easy detecting collisions with buttons. It was then a case of creating scripts that handled things like tab systems for swapping active model groups, or swapping and applying the chosen planetary ring.

I also created the system for choosing colours from a 'Colour Ring'. The colour ring uses a source image and the colour is set when the player taps the colour they want. The pixel where the user touches the colour ring is then sampled and the colour of that pixel is set as the custom colour. The below snippet is the function used for this:

<details>
  <summary>Show Code</summary>
  
    [View full image.](https://github.com/aSheedy99/SoularVRProject/blob/edd58203dab4c2b792333ce69a9c67d0a293f9c1/docs/assets/GetColourCarbonSnippet.png)
  
<p align="center">
  <img src="docs/assets/GetColourCarbonSnippet.png">
</p>
  
</details>


&nbsp;
## User Journey

With the aim of being a creative sandbox for players to experience as they wish, with no guiding narrative or strict flow of content, the user journey of Soular is fairly open. That being said, there is still a general user journey we had in mind when designing Soular that most users will likely follow:

<details>
  <summary>Show Journey</summary>
  
  [View full image.](https://github.com/aSheedy99/SoularVRProject/blob/91d393ff3e7897412c77b7cd7f7b38d2e52cd454/docs/assets/UserJourney.png)
  
<p align="center">
  <img src="docs/assets/UserJourney.png">
</p>
  
</details>
