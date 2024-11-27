# Pulse Player Developer Guide

*This document describes how to integrate Pulse Player into a page, how to configure and control it*

> Updated: Nov 22, 2024
> Document version: 2.5

## Integration

In order to integrate player into your page, place the player `iframe` tag into your HTML page.

Player tag looks like:

```html
<script src="https://trinitymedia.ai/player/pulse-js/<UNIT_ID>/?playlist=<PLAYLIST_URL>"></script>
<div class="trinity-pulse-pb" style="font:10px/18px Verdana,Arial;display:flex;justify-content:flex-end;margin-right:5px">
  <strong style="font-weight:400;margin: 0 3px 0 0">Powered by</strong>
  <a href="https://trinityaudio.ai" style="color:#4b4a4a;text-decoration:none;font-weight:700">trinityaudio.ai</a>
</div>
```

In case of putting Pulse on article page, just remove `playlist`, and we'll render article based on your page's
metadata.

```html
<script src="https://trinitymedia.ai/player/pulse-js/<UNIT_ID>/"></script>
<div class="trinity-pulse-pb" style="font:10px/18px Verdana,Arial;display:flex;justify-content:flex-end;margin-right:5px">
    <strong style="font-weight:400;margin: 0 3px 0 0">Powered by</strong>
    <a href="https://trinityaudio.ai" style="color:#4b4a4a;text-decoration:none;font-weight:700">trinityaudio.ai</a>
</div>
```

### BODY

Place the player tag wherever you'd like it to render, e.g.

```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Trinity Page Example</title>
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1" />
</head>
<body>
<div class="content">Hello!</div>
<script src="https://trinitymedia.ai/player/pulse-js/<UNIT_ID>/?playlist=<PLAYLIST_URL>"></script>
<div class="trinity-pulse-pb" style="font:10px/18px Verdana,Arial;display:flex;justify-content:flex-end;margin-right:5px">
    <strong style="font-weight:400;margin: 0 3px 0 0">Powered by</strong>
    <a href="https://trinityaudio.ai" style="color:#4b4a4a;text-decoration:none;font-weight:700">trinityaudio.ai</a>
</div>
<article></article>
<footer></footer>
</body>
</html>
```

## Tag Parameters

Pulse Player accept various query parameters, so you can change its configuration on a fly without need to change those
settings in your campaign for all players.

| Name                               | Description                                                                                                         | Rewriting unit settings? | Values                                                               |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------|--------------------------|----------------------------------------------------------------------|
| [**playlist**](#encode-parameters) | **Required**. RSS Playlist URL                                                                                      |                          |                                                                      |
| themeId                            | Set theme ID                                                                                                        | +                        |                                                                      |
| mobile                             | Set force mobile mode                                                                                               | +                        | 1/0                                                                  |
| browseMode                         | Set browse mode                                                                                                     | +                        | play, browse                                                         |
| language                           | i18n                                                                                                                | +                        | en, it, uk, etc                                                      |
| expandedURL                        | custom link for expand icon in top right. By default - it's playlist share URL based on playlist hash               | -                        |                                                                      |
| expandedURLTarget                  | Where to open expanded link. By default it's open in a new tab (_blank). But can be open on the same page (_parent) | -                        | _blank (default, new tab), _parent (same page where Pulse player is) |

## API

The Trinity Player provides a simple API for reading its status and controlling it. It's exposed via the global variable `window.TRINITY_PULSE`.
Each method has `getSignature()` method that returns its signature.

| Property                           | Type     | Description                                                                                                                                                                                |
|------------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| api                                | Object   | API methods                                                                                                                                                                                |
| api.pause(playerId)                | Function | Pause a specific player                                                                                                                                                                    |
| api.play(playerId)                 | Function | Play a specific player. **Please note, it will work only if the user has already clicked play at least once during this session on the page. Otherwise, the browser will throw an error.** |
| api.pauseAll()                     | Function | Pause all players                                                                                                                                                                          |
| api.getFirstPlayer()               | Function | Returns the first player's id, e.g. 945a52a1149c91eee4b167958b51e406                                                                                                                       |
| api.createPlayer(playerId)         | Function | (Re)create the player for a certain playerId. Please note that the `playerId` should exist in the `TRINITY_PULSE.players` object. `playerId` is optional                                   |
| api.removePlayer(playerId)         | Function | Remove a player specified by `playerId`. The `playerId` parameter is optional                                                                                                              |
| api.nextTrack(playerId)            | Function | Play/go to next track                                                                                                                                                                      |
| api.previousTrack(playerId)        | Function | Play/go to previous track                                                                                                                                                                  |
| api.setTrack(guid, playerId)       | Function | Play/go to specific audio track by `GUID`                                                                                                                                                  |
| api.setVolume(volume, playerId)    | Function | Set audio volume for player                                                                                                                                                                |
| api.getVolume(playerId)            | Function | Get audio volume for player                                                                                                                                                                |
| api.setCurrentTime(time, playerId) | Function | Set current audio position in seconds                                                                                                                                                      |
| api.getCurrentTime(playerId)       | Function | Get current audio position in seconds                                                                                                                                                      |
| players                            | Object   | Players configuration                                                                                                                                                                      |
| players[playerId]                  | Object   | Configuration of a player under a certain Id                                                                                                                                               |
| isLoaded                           | Boolean  | indicates if the Trinity initial script has been loaded                                                                                                                                    |

#### Events

*NOTE: In case abtest is enabled every event will contain abtest name in the message body*

| Event name (action)                                     | Description                                                                                                                                                           |
|---------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| injectorImp                                             | when injector script is loaded, and `TRINITY_PULSE` is ready                                                                                                          |
| TRINITY_PULSE.message.playerReady                       | Player is ready for use                                                                                                                                               |
| TRINITY_PULSE.message.playClicked                       | Play is clicked                                                                                                                                                       |
| TRINITY_PULSE.message.pauseClicked                      | Pause is clicked                                                                                                                                                      |
| TRINITY_PULSE.message.resumed                           | Player resumed                                                                                                                                                        |
| TRINITY_PULSE.message.contentStarted                    | Audio content started                                                                                                                                                 |
| TRINITY_PULSE.message.onFirstQuartile                   | Audio content is 25% complete                                                                                                                                         |
| TRINITY_PULSE.message.onMidPoint                        | Audio content is 50% complete                                                                                                                                         |
| TRINITY_PULSE.message.onThirdQuartile                   | Audio content is 75% complete                                                                                                                                         |
| TRINITY_PULSE.message.onComplete                        | Audio content is completed                                                                                                                                            |
| TRINITY_PULSE.message.adOpp                             | Ad being requested                                                                                                                                                    |
| TRINITY_PULSE.message.onAdStarted                       | Ad is started                                                                                                                                                         |
| TRINITY_PULSE.message.onAdComplete                      | Ad is completed                                                                                                                                                       |
| TRINITY_PULSE.message.touchStart                        | Touch started (mobile only)                                                                                                                                           |
| TRINITY_PULSE.message.touchEnd                          | Touch ended (mobile only)                                                                                                                                             |
| TRINITY_PULSE.message.scrubbing                         | Audio scrubbed                                                                                                                                                        |
| TRINITY_PULSE.message.updateMediaMetadata               | When [MediaMetadata](https://developer.mozilla.org/en-US/docs/Web/API/MediaMetadata) has been updated with cover image, title, author, etc                            |
| TRINITY_PULSE.message.mediaSessionAction                | When a media control action, such as play, pause, next, previous, seek is performed using external interfaces like the Control Center or other media session handlers |
| TRINITY_PULSE.message.browseModeToggleView              | When player toggle from one view mode to another. Used only when toggleMode is used                                                                                   |
| TRINITY_PULSE.message.browseModeToggleViewTransitionEnd | When toggleMode is used and animation is enabled, fires when animation is finished                                                                                    |

#### Encode parameters

```js
// https%3A%2F%2Fexample.com%2Frss
encodeURIComponent('https://example.com/rss');
```
