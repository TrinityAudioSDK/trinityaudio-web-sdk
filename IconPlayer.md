# Trinity Audio Icon Player Expandable mode Integration Guide

*This document describes how to integrate the Trinity Audio Player into a page as in icon player mode well as how to configure and control it*

> Updated: Mar 7, 2024
> Document version: 1.0

## Integration

Insert script tag in certain place (see example below) and provide placeholder where player should appear.
Please note, that player in order to work in `icon-expandable` mode, it should be configured in theme (please approach support for that) or
`playerType=icon-expandable` should be passed to script tag. But in last case - will be applied only default values.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Trinity Page Example</title>
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1"/>
    <style>
        .button-placeholder {
            display: flex; /* for example purpose */
        }

        .trinity-tts-icon-player-button-wrapper {
            width: 24px; /* set width of icon that is used in theme in order to avoid jumping. By default it's 24px */
            height: 24px; /* set height of icon that is used in theme in order to avoid jumping. By default it's 24px */
        }
    </style>
</head>
<body>
    <div class="button-placeholder">
        <button>button 1</button>
        <button>button 2</button>

        <!-- wrap with trinity-tts-icon-player-button-wrapper class -->
        <div class="trinity-tts-icon-player-button-wrapper">
            <script src="https://trinitymedia.ai/player/trinity/XXXXXXX/?pageURL=YOUR_ENCODED_PAGE_URL_HERE&playerType=icon-expandable"
                    charset="UTF-8"></script>
        </div>

        <button>button 3</button>
        <button>button 4</button>
    </div>

    <h1>Title</h1>

    <!-- use trinity-tts-placeholder-icon-player class -->
    <div class="trinity-tts-placeholder-icon-player">
        <!-- player will be rendered here -->
    </div>

    <div class="content">Hello!</div>
</body>
</html>
```
