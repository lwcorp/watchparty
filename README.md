As [defined in Wikipedia](https://en.wikipedia.org/wiki/Social_viewing):

>**Social viewing** (also known as **Watch Party** or **GroupWatch**) describes a recently developed practice revolving around the ability for multiple users to aggregate from multiple sources and view online videos together in a synchronized viewing experience. Typically the experience also involves some form of instant messaging or communication to facilitate discussion pertaining to the common viewing experience.

# Goals
This project was made exactly for this experience with some goals in mind:
1. Allowing both the host and the viewers to watch the same screen (whereas usually the host controls the video without actually seeing it).
1. Relying on pure HTML5 `<video>` usage.
1. Supporting **SRT** subtitles/captions (known in HTML5 videos as `track`s).
1. Supporting (foreign) non Unicode subtitles.
1. Only relying on client side Vanilla JS code, so anybody could use it without installing anything.
1. Allowing to choose a margin for the subtitles, as **some TVs cut them off** if they're stuck to the default bottom.
1. Including a 1 sided chat (to be shown over Chromecast) plus a bot.

# Usage
1. Choose a local video.
1. (Optionally) Choose local subtitles/captions.
1. (Optionally) Choose a margin subtitles/captions. Negative means from the player's bottom and Positive means from the player's top.
1. (Optionally) set the host's name for the chat.
1. (Optionally) [Cast the tab or screen to Chromecast](https://support.google.com/chromecast/answer/3228332) (keep in mind in Chromecast only the host has control).
1. Enjoy the social viewing!

# History
Goals 2-5 goals clashed because `track` not only doesn't support non Unicode, it only supports VTT subtitles and **not** local ones. In other words, you have to both convert your regular SRT subtitles into Unicode, then into VTT, then upload them and use online links instead of just your computer files.

Goal 3 was specifically challenging as `track` seemingly doesn't have a built-in way to set margin.

The last goal was problematic because practically almost all chats out rely on servers, while it's a complete overkill if only the host gets to chat anyway (as the rest just see it over Chromecast).

This was handled by:
1. Using `URL.createObjectURL` to convert the subtitles into `blob`s and thus bypass `track`'s server requirement.
1. Combining [SRT-Support-for-HTML5-videos](https://github.com/codeit-ninja/SRT-Support-for-HTML5-videos) with [Detect-File-Encoding-And-Language](https://github.com/gignupg/Detect-File-Encoding-And-Language).
1. Running a loop to change the subtitles/captions' margin by modifying `textTracks`' `cues`' `line`.
1. Designing an upgraded version of [Simple Chat UI](https://codepen.io/sajadhsm/pen/odaBdd) to make it more dynamic, support iframe integration and include a bot.

These actions are all event driven so that the user can change the video, subtitles/captions and margin setting at all times.

# Notes
This project can't compete with [this watchparty project](https://github.com/howardchung/watchparty) which has many other features.
However, the project here also has advanages:
1. It's new whereas the aforementioned project died more than a year ago.
1. It supports [Play/Pause when clicking the central video](https://github.com/howardchung/watchparty/issues/509) / [Clicking Pause causes a mute (but clicking Play doesn't cause an unmute)](https://github.com/howardchung/watchparty/issues/681) - both fixed in their source code by now, but not in their official release yet.
1. There's no [white overlay after subtitles/captions were uploaded](https://github.com/howardchung/watchparty/issues/510) - in fact, there's no uploading!
1. It supports [Control subtitle/caption line position/margin](https://github.com/howardchung/watchparty/issues/511).

# Screenshot
![image](https://user-images.githubusercontent.com/1773306/178153606-408892ff-e80f-4513-aa15-114b6d4bc769.png)
