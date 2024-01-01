# Pulse Player Developer Guide

*This document describes how to integrate Pulse Player into a page, how to configure and control it*

> Updated: Dec 21, 2023
> Document version: 2.0

## Integration

In order to integrate player into your page, place the player `iframe` tag into your HTML page.

Player tag looks like:

```html
<script src="https://trinitymedia.ai/player/pulse-js/<UNIT_ID>/?playlist=<PLAYLIST_URL>&pageURL=<PAGE_URL>"></script>
<div class="trinity-pulse-pb" style="font:10px/18px Verdana,Arial;display:flex;justify-content:flex-end;margin-right:5px">
  <strong style="font-weight:400;margin: 0 3px 0 0">Powered by</strong>
  <a href="https://trinityaudio.ai" style="color:#4b4a4a;text-decoration:none;font-weight:700">trinityaudio.ai</a>
</div>
```

In case of putting Pulse on article page, just remove `playlist`, and we'll render article based on your page's
metadata.

```html
<script src="https://trinitymedia.ai/player/pulse-js/<UNIT_ID>/?pageURL=<PAGE_URL>"></script>
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
<script src="https://trinitymedia.ai/player/pulse-js/<UNIT_ID>/?playlist=<PLAYLIST_URL>&pageURL=<PAGE_URL>"></script>
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
| [**pageURL**](#encode-parameters)  | **Required**. Current page URL                                                                                      |                          |                                                                      |
| themeId                            | Set theme ID                                                                                                        | +                        |                                                                      |
| mobile                             | Set force mobile mode                                                                                               | +                        | 1/0                                                                  |
| browseMode                         | Set force browse mode                                                                                               | +                        | 1/0                                                                  |
| language                           | i18n                                                                                                                | +                        | en, it, uk, etc                                                      |
| expandedURL                        | custom link for expand icon in top right. By default - it's playlist share URL based on playlist hash               | -                        |                                                                      |
| expandedURLTarget                  | Where to open expanded link. By default it's open in a new tab (_blank). But can be open on the same page (_parent) | -                        | _blank (default, new tab), _parent (same page where Pulse player is) |

#### Encode parameters

```js
// https%3A%2F%2Fexample.com%2Frss
encodeURIComponent('https://example.com/rss');
```
