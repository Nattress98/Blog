---
layout: post
title: Zero Gravity VR Player Controller
---

![Echo Arena Gif]({{ site.baseurl }}/images/echo_arena_goal.gif?){.header-img}

-- http://www.twitch.tv/videos/162630473?t=3s --

Hi, over the past week or two I've had a lot of spare time on my hands, COVID-19 has me caged up at home. A lot of that time I've spent playing echo arena on the quest with friends. I've always loved competitive games and echo arena is no exception, it's fast paced and I love many of the design choices. Inspired by the creative method of locomotion, I decided to replicate it in Unity, and do a little writeup on how I achieved the effect.

I started with a new project and a piece of paper, I sketched different stages to how controller should perform in each circumstance. I determined that when a player grabs the wall the hand mesh should attach to the wall and the player's velocity should be set to zero. Then, while the player holds onto the wall I should track the change in position of the controller every frame, as the controller should move the camera using it. While grabbing a wall, the camera should move closer to the hand when the controller is moved towards the hmd. This means subtracting the controller's delta position from the camera's current position. I do this to the parent as at this point the hands position is locked and we can control the player with one rigidbody.

When the grip is released the camera's current velocity needs to be maintained, to allow for the player to launch off walls. To do this, I just apply the velocity (calculated from the hand delta position / Time.fixedDeltaTime * -1.0f). In a real release, you might want to experiment with smoothing the release velocity e.g. an average of the past 10 frames, I haven't tried so I don't know if this improves the result.

I decided not to complicate things with camera roll as it can cause lots of discomfort to people and in my opinion take away from immersion. I am not fully decided on what I'll use this for, however I am currently planning to test it with a weapons system I built in the past and see how that feels.
