---
layout: post
title:  "Playing Audio using Swift 2 & AVFoundation"
date:   2016-02-13 10:49:38 +0530
author: Akshar Patel
---



Todo:

- Playing Audio
- Recording & Storing Audio
- Mixing the Audio for Special Effects

Next we'll add Recording Abilities.


{% highlight swift %}
import AVFoundation

// Setting the path where the audio file to be played, exists.
let audioUrl = NSURL()

//TODO: Setting up Audio Session. This is required to play the audio.

let audioPlayer = AVAudioPlayer()

// To Play the Audio
audioPlayer.play()

// To change the rate at which audio plays
audioPlayer.rate = 1.0 

// To Stop the Audio
audioPlayer.stop()

{% endhighlight %}