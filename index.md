## What Is Soular VR?

<p align="center">
  <img src="/docs/assets/SoularVRBlankPlanet.png?raw=true" alt="An empty, white, planet-like object hovers in mid-air. A ring-shaped table holds different coloured paints on the right, with the label 'Palette', and on the right, multiple buttons with the label 'Models'"/>
</p>

Soular VR is an creative environment built for Meta Quest 2 that allows players to shape entire worlds with their own hands! This page will explore my contribution to the project, formatted in a chronological timeline and ending with a reflection. Soular was made as the final project for Goldsmith's MSc XR course. As well as myself, the piece was created by Seonjeong Park (Technical), Ebba Liepe (Art) and Nicalia ThompSon (Art). Soular was built in Unity using Meta's OVR Plugin.

&nbsp;
### Player Gestures

My main task for this project was creating a flexible and performant system capable of recording hand gestures as recognisable inputs using Meta's OVR Plugin for Unity. The following code is essentially the final function used for this (although it has been simplified for ease of reading):

```

//This function compares the current positions relative to the first bone in the list with the same data from a recorded gestures, and optionally the rotation of the first bone to the head

//This list contains all the positions described previously for a recorded gesture
List<Vector3> HandBones;


float minDistance = infinity, distanceTotal;

///check each bone in a given hand
for(HandBones.Count) 
{
  //this gets the current relative position of a bone
  Vector3 currentBonePosition = currentHandSkeleton.transform.InverseTransformPoint(HandBones[i].Transform.position);
  
  //calculate the distance between the current relative position and the recorded relative position
  float distance = (currentBonePosition - HandBones[i]).sqrMagnitude;
  
  //check if this distance is below a developer-defined threshold, 
  //if so the current gesture is too different from the recorded gesture
  if(distance > tolerance * tolerance) return;
  
  //if it was not too far away, add this distance to the distance total
  distanceTotal += distance;
}

//Optionally, check the rotation of the current hand against the recorded rotation
if(shouldCheckRotation) 
{
  Quaternion relativeRotation = Quaternion.Inverse(HandBones[0].Transform.roation) * headRotation;
  
  float angularDifference = Quaternion.Angle(relativeRotation, recordedRotation);
  
  //if the angular difference between the two rotations is greater than the tolerance, then a match has not been found
  if(angularDifference > rotationalTolerance) return;
}

```

