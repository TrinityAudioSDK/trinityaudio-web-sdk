# Trinity Audio Icon Player Integration Guide

*This document provides a detailed guide for integrating the Icon Player.*

> Updated: Jan 22, 2025
> Document version: 2.0

## Overview

The Icon Player is a compact player that can be embedded anywhere on a webpage. When clicked, it opens a full TTS player in a specified position or as a sticky player at the bottom of the page. It supports single-click activation and various themes.

## Integration Steps

### Step 1: Contact Trinity Audio Support

To configure the Icon Player, contact our support team. Specify whether you want the player in a fixed position or as a sticky player at the bottom. Discuss any theme preferences before proceeding.

### Step 2: Insert the Script Tag

Determine the position for the icon and insert the script tag there. 
Assign the following class name: `trinity-tts-icon-player-button-wrapper`. Example:

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

Create a placeholder where the TTS player will appear when the Icon Player is clicked. 
Assign the following class name: `trinity-tts-placeholder-icon-player`. 
This step is required even if the player loads as a sticky player at the bottom. 
Example:

```html
<body>
    <h1>Title</h1>

    <!-- Use trinity-tts-placeholder-icon-player class -->
    <div class="trinity-tts-placeholder-icon-player">
        <!-- Player will be rendered here -->
    </div>

    <div class="content">Hello!</div>
</body>
```