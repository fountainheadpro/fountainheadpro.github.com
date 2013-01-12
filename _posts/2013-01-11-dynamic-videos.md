---
layout: post
title: "Technology for interactive stories: Dynamic videos"
description: ""
category: 
tags: []
---
{% include JB/setup %}

At [ForUs](http://forusall.com){:target="_blank"}, we are building engaging and interactive conversations, which educate people about ways to handle their financial situation. 

Unlike regular educational video, where the viewer takes passive role, we build interactive conversations. The user is presented with the set educational materials and questions, which they can answer. The conversation flow depends on user answers.

* This will become a table of contents (this text will be scraped).
{:toc}

Right now I'm experimenting with various ways to utilize the technology to tell the story. Here are some interesting lessons learned. This post is about using different videos for each scene.

#Presenting user choices
Once the video scene is over, I need to react and present the choices to a user. Question was, how do I know that the video is over? 

First attempt to use the video [ended](http://www.longtailvideo.com/html5/playback/){:target="_blank"} event and present user choices at the moment, when the video stopped playing.This one did not work. When building interactive interactive conversations, user last scene presents an opportunity to naturally bring user choices, so the user feels naturally feels like prompts are the part of the experience. So the video needs to be stopped on the last scene. The default behavior of the player is to auto-rewind the video to the first frame once it's stopped playing.

To solve this problem, I had to use timeupdate event and pause the video on the last scene. We had to make the last significant scene a second before the video ends.

{% highlight javascript %}
  timeupdate: function(e) {
    var max_duration;
    max_duration = this.vPlayer.duration() - 1;
    if (max_duration > 0 && this.vPlayer.currentTime() > max_duration) {
      this.vPlayer.pause();
      return this.$el.trigger('finished_scene');
    }
  }
{% endhighlight%} 

The container listening to the events "finished_scene" will be presenting user choices. 

#Stitching videos together
First lesson, learned about dynamically building a conversation from video's is that swapping video's is not as easy as swapping other DOM elements. Video is played as part of the video player and 
dynamically reloading the video player instance on every new video will not produce satisfactory user experience. It produces ugly flicks, which break user engagement with the story. 
I used [video.js](http://http://videojs.com/){:target="_blank"}, which is open source and has reasonably good documentation.

I noticed flickering, which break the user engagement. The solution was fairly simple, but not obvious. 

1. Instead of reloading the player I started reloading the video source, while the instance of the player stayed the same.
2. After modifying the source, I found that the video player still was in pause mode and the way to play the video after the source was changed was only by calling play() method.
3. Video player still works as the video tape, which needs to be rewind.

Here is the final script, which I use to reset video player before swapping source:

{% highlight javascript %}
  reset_player: function() {
    if (this.vPlayer.currentSrc()) {
      this.vPlayer.currentTime(0);
      return this.vPlayer.play();
    }
  }
{% endhighlight %}

#Optimizing video load 
Main challenge, we found on the quest to keep the user engaged in the interactive conversation was video load speed. The each portion of the video needs to start playing instantly. We found that 360p video resolution delivers acceptable load speed for average users.
Going higher quality will not work. 

In order to understand the real user experience, I measured the timing between the moment I request video play, till the moment the user see the first frame. In order to capture the moment, when the video starts playing I use *play* event, which is fired the moment the video loading is complete and the user see the first frame. 

I also [mixpanel](http://www.mixpanel.com){:target="_blank"} to aggregate the metrics.

We consider acceptable video load performance to be between 0.5 and 1 second. This speed allows the video conversation to go smoothly with no noticeable delays.

Our experiments demonstrated that ETA can not be achieved consistently using traditional cloud providers. In order to consistently deliver achieve this ETA, I'm working on video pre-loading technology, which will allow loading videos for further interactions while the user is engaged with previous steps.

**Final remarks**: Here is the page to learn more about HTML5 video and events: [http://www.w3.org/2010/05/video/mediaevents.html] 
