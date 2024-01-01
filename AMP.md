# Trinity Audio Player AMP Integration Guide

> Updated: July 20, 2022
> Document version: 3.2

This document describes how to integrate Trinity Audio Player into an AMP page using AMP standard components. Instructions are provided here on how to configure and control it.

Include the following code in the AMP layout while providing the `src` to point to trinitymedia.ai endpoint and `data-param-url` to point to the content page.

When loading a page, our player will fetch the page content first using the `data-param-url` and then load the player with the most up-to-date content instantly. This "double" rendering to access the page content is required to adhere to AMPs strict access control.

**PLEASE NOTE:**
- Page content must be fetched twice. The first one happening when displaying the page content to the user. The second will be performed by the player to fetch the content
- CORS should be enabled (ensure that reading page returns `Access-Control-Allow-Origin: *` header)
- **Important note**: Dynamic content is not supported. Content should be provided via HTML source (will fit most AMP implementations).

```html
<head>
    <!-- Make sure the script below is included -->
    <script async custom-element="amp-video-iframe" src="https://cdn.ampproject.org/v0/amp-video-iframe-0.1.js"></script>
</head>
<body>
    <amp-video-iframe
        class="trinity-player"
        src="https://trinitymedia.ai/player/trinity-amp/[YOUR_UNIT_ID]/"
        data-param-url="[CONTENT_URL]"
        layout="fixed-height"
        height="80"
    ></amp-video-iframe>
</body>
```

### Required Parameters
The following parameters are required for the player to render successfully:

| Name | Description | Values |
|:-|:-|:-|
| **src** | https://trinitymedia.ai/player/trinity-amp/[YOUR_UNIT_ID]/ | e.g. 2900000001 |
| **data-param-url**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; | URL of your page. Should be your page URL even if a page served from Google AMP Cache | e.g. https://example.com/page-1 |

It is especially important to verify that the **`data-param-url`** parameter will access the same page the Trinity Player is rendered on.

<br/>
<br/>

## Additional Player Parameters

Trinity player supports multiple options for on-page configuration and customization. This is a small sample.

For the full list of parameters see [TTS player documentation](https://trinity-audio-player.s3.amazonaws.com/TTS.pdf#script-tag-parameters) section `Script Tag Parameters`. Note that parameters name should be converted to **kebab-case** and prefixed with **data-param-**. For example:

`abtest` ==> `data-param-abtest`

`language` ==> `data-param-language`

`voiceGender` ==> `data-param-voice-gender`

`publisherUserId` ==> `data-param-publisher-user-id`

`multipleArticlesAlg` ==> `data-param-multiple-articles-alg`

`adMaxDurationAllowed` ==> `data-param-ad-max-duration-allowed`


### Example

```html
<amp-video-iframe
    class="trinity-player"
    src="https://trinitymedia.ai/player/trinity-amp/[YOUR_UNIT_ID]/"
    data-param-url="[CONTENT_URL]"
    data-param-abtest="[AB_TEST_NAME]"
    data-param-language="es"
    data-param-voice-gender="f"
    data-param-publisher-user-id="[USER_ID]"
    data-param-multiple-articles-alg="byContentStarted"
    data-param-ad-max-duration-allowed="30"
    layout="fixed-height"
    height="80"
></amp-video-iframe>
```

## AMP Analytics

The player emits multiple events that indicate user interactions and player state. You can register to these events and use them for your own analytics platform by using an `amp-analytics` component. For example - this code snippet shows tracking of these events to a google analytics account. Every event needs to be prefixed with **`video-custom-`** in order to be subscribed on in `amp-analytics` trigger.

Additional event data is to be defined in `extraUrlParams` amp-analytics section with **`custom_`** prefix.

For the up to date list of events see [TTS player documentation](https://trinity-audio-player.s3.amazonaws.com/TTS.pdf#evemts) section `Events`.

### Example

```html
<amp-analytics type="googleanalytics">
    <script type="application/json">
    {
        "vars": {
            "account": "UA-XXXXX"
        },
        "triggers": {
            // Tracking events with no additional data
            "playClicked": {
                "on": "video-custom-playClicked",
                "selector": ".trinity-player",
                "request": "event"
            },
            "onComplete": {
                "on": "video-custom-onComplete",
                "selector": ".trinity-player",
                "request": "event"
            },
            // Tracking events with additional data
            "contentStarted": {
                "on": "video-custom-contentStarted",
                "selector": ".trinity-player",
                "request": "event",
                "extraUrlParams": {
                    "duration": "${custom_duration}",
                    "src": "${custom_src}"
                }
            },
            "scrubbing": {
                "on": "video-custom-scrubbing",
                "selector": ".trinity-player",
                "request": "event",
                "extraUrlParams": {
                    "from": "${custom_from}",
                    "to": "${custom_to}"
                }
            }
        },
        // Vars are being applied to every trigger. Current example will be sent to analytics platform as query params:
        // ec=general&el=trinity-player&ea=[eventAction]
        // where "ea" will correspond to the event action name of "video-custom-[eventAction]"
        "vars": {
            "eventCategory": "general",
            "eventLabel": "trinity-player",
            "eventAction": "${custom_eventAction}"
        }
    }
    </script>
</amp-analytics>

<amp-video-iframe
    class="trinity-player"
    src="https://trinitymedia.ai/player/trinity-amp/[YOUR_UNIT_ID]/"
    data-param-url="[CONTENT_URL]"
    layout="fixed-height"
    height="80"
></amp-video-iframe>
```
### Analytics events list

| Name | Description | Additional Event Data |
|:-|:-|:-|
| video-custom-playerReady | player is ready to use |
| video-custom-enteredView | player show up initially or after being hidden |
| video-custom-playClicked | Play button clicked for the first time |
| video-custom-contentStarted | content playback started | duration, src |
| video-custom-adOpp | ad being requested |
| video-custom-onAdStarted | ad playback started |
| video-custom-onAdComplete | ad playback ended |
| video-custom-pauseClicked | Pause button clicked |
| video-custom-resumed | Play button clicked after player being paused |
| video-custom-scrubbing | scrubbing performed | from, to |
| video-custom-onFirstQuartile | 25% of playback has passed |
| video-custom-onMidPoint | 50% of playback has passed |
| video-custom-onThirdQuartile | 75% of playback has passed |
| video-custom-onComplete | 100% of playback has passed. Current content playback is completed |
