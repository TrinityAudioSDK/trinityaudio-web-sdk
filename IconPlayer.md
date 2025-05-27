# Trinity Audio Icon Player Integration Guide

*This document provides a detailed guide for integrating the Icon Player.*

> Updated: May 26, 2025
> Document version: 2.1

## Overview

The Icon Player is a compact player that can be embedded anywhere on a webpage.\
When clicked, it opens a full TTS player in a specified position or as a sticky player at the bottom of the page.\
It supports single-click activation and various themes.

## Integration Steps

### Step 1: Contact Trinity Audio Support

To configure the Icon Player, contact our support team. Specify whether you want the player in a fixed position or as a sticky player at the bottom. Discuss any theme preferences before proceeding.

### Step 2: Insert the Script Tag

Determine the position for the icon and insert the script tag there.\
Assign the following class name: `trinity-tts-icon-player-button-wrapper`.\
\
Example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Trinity Page Example</title>
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1"/>
    <style>
        .button-placeholder {
            display: flex; /* Example purpose */
        }

        .trinity-tts-icon-player-button-wrapper {
            width: 24px; /* Set icon width to avoid jumping, default is 24px */
            height: 24px; /* Set icon height to avoid jumping, default is 24px */
        }
    </style>
</head>
<body>
    <div class="button-placeholder">
        <button>button 1</button>
        <button>button 2</button>

        <!-- Wrap with trinity-tts-icon-player-button-wrapper class -->
        <div class="trinity-tts-icon-player-button-wrapper">
            <script src="https://trinitymedia.ai/player/trinity/XXXXXXX/?pageURL=YOUR_ENCODED_PAGE_URL_HERE"
                    charset="UTF-8"></script>
        </div>

        <button>button 3</button>
        <button>button 4</button>
    </div>
</body>
</html>
```

### Step 3: Add a Placeholder for the TTS Player

Create a placeholder where the TTS player will appear when the Icon Player is clicked.\
Assign the following class name: `trinity-tts-placeholder-icon-player`.\
This step is required even if the player loads as a sticky player at the bottom.\
\
Example:

```html
<body>
    <h1>Title</h1>

    <!-- Use trinity-tts-placeholder-icon-player class -->
    <div class="trinity-tts-placeholder-icon-player">
        <!-- Player will be rendered over that element -->
    </div>

    <div class="content">Hello!</div>
</body>
```

## Integration Steps for Multiple Players

To integrate the Icon Player using the [Multiple Player approach](https://github.com/TrinityAudioSDK/trinityaudio-web-sdk/blob/main/TTS.md#multiple-players), please refer to the [RCH](https://github.com/TrinityAudioSDK/trinityaudio-web-sdk/blob/main/TTS.md#read-content-hook)\
\
Ensure the following requirements are met:

1. Each script must include a `data-player-id` attribute (as required for the Multiple Players setup)
2. Each `.trinity-tts-icon-player-button-wrapper` element must also include a `data-player-id` attribute
3. Provide a placeholder element where the player should be rendered. Use the class `.trinity-tts-placeholder-icon-player` and include the corresponding `data-player-id` attribute for each instance

Example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Trinity Page Example</title>
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1"/>
    <style>
        .button-placeholder {
            display: flex; /* Example purpose */
        }

        .trinity-tts-icon-player-button-wrapper {
            width: 32px; /* Set icon width to avoid jumping, default is 24px */
            height: 32px; /* Set icon height to avoid jumping, default is 24px */
        }
    </style>
    <script>
        window.__trinityMultiplePlayers__ = true;
    </script>
</head>
<body>
    <!-- article 1 -->
    <div class="button-placeholder">
        <button>button 1</button>

        <!-- Wrap with trinity-tts-icon-player-button-wrapper class with data-player-id attribute -->
        <div class="trinity-tts-icon-player-button-wrapper" data-player-id="player-1">
            <script src="https://trinitymedia.ai/player/trinity/XXXXXXX/?pageURL=YOUR_ENCODED_PAGE_URL_HERE"
                    data-player-id="player-1"
                    charset="UTF-8"></script>
        </div>

        <button>button 2</button>
    </div>

    <!-- Use trinity-tts-placeholder-icon-player class with data-player-id attribute -->
    <div class="trinity-tts-placeholder-icon-player" data-player-id="player-1">
        <!-- Player will be rendered over that element -->
    </div>

    <!-- article 2 -->
    <div class="button-placeholder">
        <button>button 1</button>

        <!-- Wrap with trinity-tts-icon-player-button-wrapper class with data-player-id attribute -->
        <div class="trinity-tts-icon-player-button-wrapper" data-player-id="player-2">
            <script src="https://trinitymedia.ai/player/trinity/XXXXXXX/?pageURL=YOUR_ENCODED_PAGE_URL_HERE"
                    data-player-id="player-2"
                    charset="UTF-8"></script>
        </div>

        <button>button 2</button>
    </div>

    <!-- Use trinity-tts-placeholder-icon-player class with data-player-id attribute -->
    <div class="trinity-tts-placeholder-icon-player" data-player-id="player-2">
        <!-- Player will be rendered over that element -->
    </div>

    <!-- article 3 -->
    <!-- ... -->
</body>
</html>
```
