---
layout: post
title:  "Playing Audio Files using Swift 2 & AVFoundation"
date:   2016-02-13 10:49:38 +0530
author: Akshar Patel
---

I'll start simple. Let's see how to play Audio using Swift 2 and AVFoundation framework.

The first thing we do is import AVFoundation framework at the top of the Swift file.
{% highlight swift %}
import AVFoundation
{% endhighlight %}

Add the Audio File to your project by right clicking the folder in the Project
Navigator and clicking on `Add file to Your_Project`.

We'll now get the path to the audio file and create it's url using
{% highlight swift %}
let audioPath = NSBundle.mainBundle().pathForResource("file_name", ofType: "mp3")
let audioURL = NSURL(fileURLWithPath: audioPath!)
{% endhighlight %}

Next, we'll setup our Audio Player and play the audio.

{% highlight swift %}
let audioPlayer = AVAudioPlayer(contentsOfURL: audioURL)
audioPlayer.play()
{% endhighlight %}

That's it. This plays the audio file in your app.

There are a few methods available to AVAudioPlayer instance that are worth mentioning
{% highlight swift %}
// To pause the Audio
audioPlayer.pause()
// To stop the Audio
audioPlayer.stop() 
// To change the playback rate of the audio being played
audioPlayer.rate = 0.5 // Available range is [0.5, 2.0]
{% endhighlight %} 

Both the pause() and stop() methods stop current playback. The playback picks up from the last 
point when play resumes. To start from the beginning upon stopping the
audioPlayer:
{% highlight swift %}
// Stop the audioPlayer
audioPlayer.stop()
// Change the playback point of the audio to the start
audioPlayer.currentTime = 0.0 // This could be used to add seek functionality to the audioPlayer by 
// combining it with a slider
{% endhighlight %}

**Software Used**

- Swift 2.1
- Xcode 7.2

To know more about the AVAudioPlayer, have a look at its documenation [here](https://developer.apple.com/library/ios/documentation/AVFoundation/Reference/AVAudioPlayerClassReference/).

