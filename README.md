<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/sunlightx/xal-reverse">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Epic_Games_logo.svg/1200px-Epic_Games_logo.svg.png" alt="Logo" width="150" height="150">
  </a>

  <h3 align="center">Epicgames Xal Reverse</h3>

  <p align="center">
    Reversed New Epicgames XAL encryption algorithm.
</div>

### Important Notes

The encryption algorithm uses two important values that **periodically change** with Epic Games updates:

1. **`f476()` - Encryption Key (32 bytes)**

   - This function returns a 32-byte encryption key used for ChaCha20 encryption
   - The key values change with Epic Games updates
   - You must update these values in `Xal.js` when they change

2. **`f478()` - Nonce/IV (3 Uint32 values)**
   - This function returns 3 Uint32 values used as nonce/initialization vector for ChaCha20
   - These 3 values also change with Epic Games updates
   - Must be updated alongside the encryption key

**How to update:**

1. **Finding the Encryption Key (`f476()`):**

   - Search for the pattern `"))));"` in the Epic Games Talon-Sdk JavaScript file
   - Read the line from right to left (backwards)
   - The first function call you encounter is the key function (e.g., `_0xc88c11['wDhdU'](_0x52ee72)`)
   - Example:

     ```javascript
     return _0xc88c11[_0x18e4e2(0x1bb, 0x1ed)](
       _0xeac2be, {}, _0x1d2150,
       _0xc88c11[_0x18e4e2(0x1ce, 0x1fb)](
         _0x321c67, [][_0x18e4e2(0x21f, 0x22c)](
           _0xb16d9e(new Uint8Array(_0x232438[_0x18e4e2(0x251, 0x298)])),
           _0xc88c11[_0x18e4e2(0x1ce, 0x18e)](_0xb16d9e, _0x29b931(_0x39b4b0)),
           _0xb16d9e(_0x155667(_0x13272a, _0xc88c11['wDhdU'](_0x52ee72), _0x232438))
         )
       )
     );
     ```

   - In this example, `_0xc88c11['wDhdU'](_0x52ee72)` is the key function - trace it to find the 32-byte array

2. **Finding the Nonce Values (`f478()`):**

   - Search for `new Uint32Array` in the Talon-Sdk file
   - Look for arrays with exactly 3 values (you'll typically find ~6 results, but you need the one with 3 Uint32 values)
   - The pattern usually looks like: `new Uint32Array([value1, value2, value3])`
   - Example:
     ```javascript
     new Uint32Array([_0x12a225['kroEK'](0xb1ce78fe, -0x24906af1), (function() {
        function _0x3367ac(_0x7c1c43, _0x494593) {
            return _0x39e171(_0x7c1c43 - 0x1e3, _0x494593);
        }
        if (_0x3367ac(0x2aa, 0x24f) !== _0x12a225[_0x3367ac(0x355, 0x321)])
            return _0x12a225[_0x3367ac(0x324, 0x361)](0xae616c6, -0x1f76a7e9);
        _0x3603fa['f']();
     }()), -0x16aa37d])
     ```
   - `_0x12a225['kroEK'](0xb1ce78fe, -0x24906af1) = 1788997105`
   - `return _0x12a225[_0x3367ac(0x324, 0x361)](0xae616c6, -0x1f76a7e9) = -361804079`
   - `-0x16aa37d = -23765885`
   - Extract the 3 final numeric values (after evaluating any function calls) and use them in `f478()`

3. **Updating the values:**
   - Once found, update the arrays in `f476()` and `f478()` functions in `Xal.js`
   - Without correct values, the XAL encryption will not work properly

## Contact

Telegram - [@eternalbladez](https://t.me/eternalbladez)

## Example of Fingerprint

```json
{
  "0": 50,
  "1": "2026-01-05T23:51:25.518Z",
  "2": "103a739741aa26",
  "3": {
    "title": "Passwort für dein Epic Games-Konto zurücksetzen | Epic Games",
    "referrer": ""
  },
  "4": true,
  "5": {
    "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/143.0.0.0 Safari/537.36",
    "platform": "Win32",
    "language": "de-DE",
    "languages": ["de-DE", "de", "en-US", "en"],
    "hardware_concurrency": 8,
    "device_memory": 8,
    "product": "Gecko",
    "product_sub": "20030107",
    "vendor": "Google Inc.",
    "vendor_sub": "",
    "webdriver": false,
    "max_touch_points": 0,
    "cookie_enabled": true,
    "property_list": [
      "vendorSub",
      "productSub",
      "vendor",
      "maxTouchPoints",
      "scheduling",
      "userActivation",
      "geolocation",
      "doNotTrack",
      "plugins",
      "mimeTypes",
      "pdfViewerEnabled",
      "webkitTemporaryStorage",
      "webkitPersistentStorage",
      "hardwareConcurrency",
      "cookieEnabled",
      "appCodeName",
      "appName",
      "appVersion",
      "platform",
      "product",
      "userAgent",
      "language",
      "languages",
      "onLine",
      "webdriver",
      "connection",
      "getGamepads",
      "javaEnabled",
      "sendBeacon",
      "vibrate",
      "windowControlsOverlay",
      "deprecatedRunAdAuctionEnforcesKAnonymity",
      "protectedAudience",
      "bluetooth",
      "clipboard",
      "credentials",
      "keyboard",
      "managed",
      "mediaDevices",
      "storage",
      "serviceWorker",
      "virtualKeyboard",
      "wakeLock",
      "deviceMemory",
      "userAgentData",
      "locks",
      "login",
      "ink",
      "mediaCapabilities",
      "devicePosture",
      "hid",
      "mediaSession",
      "permissions",
      "presentation",
      "serial",
      "gpu",
      "usb",
      "xr",
      "storageBuckets",
      "adAuctionComponents",
      "runAdAuction",
      "canLoadAdAuctionFencedFrame",
      "canShare",
      "share",
      "clearAppBadge",
      "getBattery",
      "getUserMedia",
      "requestMIDIAccess",
      "requestMediaKeySystemAccess",
      "setAppBadge",
      "webkitGetUserMedia",
      "clearOriginJoinedAdInterestGroups",
      "createAuctionNonce",
      "joinAdInterestGroup",
      "leaveAdInterestGroup",
      "updateAdInterestGroups",
      "deprecatedReplaceInURN",
      "deprecatedURNToURL",
      "getInstalledRelatedApps",
      "getInterestGroupAdAuctionData",
      "registerProtocolHandler",
      "unregisterProtocolHandler"
    ],
    "connection_rtt": 150
  },
  "6": {
    "canvas_fingerprint": {
      "length": 38354,
      "num_colors": 4676,
      "md5": "f2348c497eafa12e4ea43bb9325303ec",
      "tlsh": "9C03F1B3323080941A61757E73C5E79C2C28EF945E8DAB9B0FE2E64111E2D07ADB4747"
    },
    "parameters": {
      "renderer": "ANGLE (NVIDIA, NVIDIA GeForce GTX 1060 3GB (0x00001B84) Direct3D11 vs_5_0 ps_5_0, D3D11)",
      "vendor": "Google Inc. (NVIDIA)"
    }
  },
  "7": {
    "location": {
      "origin": "https://www.epicgames.com",
      "pathname": "/id/login/forgot-password",
      "href": "https://www.epicgames.com/id/login/forgot-password?lang=de&redirect_uri=https%3A%2F%2Fstore.epicgames.com%2Fde&client_id=875a3b57d3a640a6b7f9b4e883463ab4"
    },
    "history": {
      "length": 2
    },
    "screen": {
      "avail_height": 1040,
      "avail_width": 1920,
      "avail_top": 0,
      "height": 1080,
      "width": 1920,
      "color_depth": 24
    },
    "performance": {
      "memory": {
        "js_heap_size_limit": 4294967296,
        "total_js_heap_size": 30305649,
        "used_js_heap_size": 27049781
      },
      "resources": [
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/Inter-Bold-CuhepTt8.woff2",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/Inter-Light-CdXm_ABL.woff2",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/Inter-Medium-P1cOs5ep.woff2",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/Inter-Regular-CKDp9E3C.woff2",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/InterTight-Bold-CPdZBAQJ.woff2",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/InterTight-Black-CBljiM1E.woff2",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/index-QoEJFRtM.js",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/index-CTGxZpYh.css",
        "https://tracking.epicgames.com/tracking.js",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/ie11-DFmH3mxD.js",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/es.array.from-BX-4vO9h.js",
        "https://www.epicgames.com/id/api/i18n?ns=messages&lang=de",
        "https://www.epicgames.com/id/api/i18n?ns=epic-consent-dialog&lang=de",
        "https://www.epicgames.com/id/api/i18n?ns=messages&lang=de",
        "https://www.epicgames.com/id/api/i18n?ns=epic-consent-dialog&lang=de",
        "https://sentry.io/api/1333512/envelope/?sentry_key=7a13b97c16f4455f92376d5c1e27f102&sentry_version=7&sentry_client=sentry.javascript.react%2F7.118.0",
        "https://www.epicgames.com/id/api/location",
        "https://www.epicgames.com/id/api/analytics",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/stable-Cp3wsz2Y.js",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/index-JJHKwImU.js",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/polyfill-B0Rz2pbH.js",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/serviceWorker-DnttpXcQ.js",
        "https://www.epicgames.com/id/api/analytics",
        "https://www.epicgames.com/id/api/client/875a3b57d3a640a6b7f9b4e883463ab4?redirectUrl=https%3A%2F%2Fstore.epicgames.com%2Fde",
        "https://www.epicgames.com/id/api/authenticate",
        "https://www.epicgames.com/id/api/analytics",
        "https://www.epicgames.com/id/api/analytics",
        "https://tracking.epicgames.com/track.png?referringUrl=none&location=https%3A%2F%2Fwww.epicgames.com%2Fid%2Flogin%2Fforgot-password%3Flang%3Dde%26redirect_uri%3Dhttps%253A%252F%252Fstore.epicgames.com%252Fde%26client_id%3D875a3b57d3a640a6b7f9b4e883463ab4&now=1767657043160&eventType=pageView",
        "https://www.epicgames.com/id/api/analytics",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/ModalBasePage-D6gPxQHC.js",
        "https://static-assets-prod.unrealengine.com/account-portal/static/assets/ForgotPasswordPage-DcUWPLXD.js",
        "https://talon-website-prod.ecosec.on.epicgames.com/talon_sdk.js",
        "https://talon-service-prod.ecosec.on.epicgames.com/v1/init",
        "https://static-assets-prod.unrealengine.com/account-portal/static/manifest.json",
        "https://js.hcaptcha.com/1/api.js?onload=hCaptchaLoaded&render=explicit",
        "https://newassets.hcaptcha.com/captcha/v1/2e2f9feae51e15dd4676ba8e3d761ec72f41b826/static/i18n/de.json",
        "https://newassets.hcaptcha.com/captcha/v1/2e2f9feae51e15dd4676ba8e3d761ec72f41b826/static/hcaptcha.html#frame=checkbox-invisible",
        "https://talon-service-prod.ecosec.on.epicgames.com/v1/phaser/batch",
        "https://sentry.io/api/1333512/envelope/?sentry_key=7a13b97c16f4455f92376d5c1e27f102&sentry_version=7&sentry_client=sentry.javascript.react%2F7.118.0",
        "https://talon-service-prod.ecosec.on.epicgames.com/v1/init/execute",
        "https://talon-service-prod.ecosec.on.epicgames.com/v1/phaser/batch",
        "https://www.epicgames.com/id/api/analytics",
        "https://www.epicgames.com/id/api/account/recovery",
        "https://talon-service-prod.ecosec.on.epicgames.com/v1/phaser/batch"
      ]
    },
    "device_pixel_ratio": 1,
    "dark_mode": true,
    "chrome": true,
    "property_list": [
      "0",
      "1",
      "2",
      "window",
      "self",
      "document",
      "name",
      "location",
      "customElements",
      "history",
      "navigation",
      "locationbar",
      "menubar",
      "personalbar",
      "scrollbars",
      "statusbar",
      "toolbar",
      "status",
      "closed",
      "frames",
      "length",
      "top",
      "opener",
      "parent",
      "frameElement",
      "navigator",
      "origin",
      "external",
      "screen",
      "innerWidth",
      "innerHeight",
      "scrollX",
      "pageXOffset",
      "scrollY",
      "pageYOffset",
      "visualViewport",
      "screenX",
      "screenY",
      "outerWidth",
      "outerHeight",
      "devicePixelRatio",
      "event",
      "clientInformation",
      "screenLeft",
      "screenTop",
      "styleMedia",
      "onsearch",
      "onappinstalled",
      "onbeforeinstallprompt",
      "crypto",
      "onbeforexrselect",
      "onabort",
      "onbeforeinput",
      "onbeforematch",
      "onbeforetoggle",
      "onblur",
      "oncancel",
      "oncanplay",
      "oncanplaythrough",
      "onchange",
      "onclick",
      "onclose",
      "oncommand",
      "oncontentvisibilityautostatechange",
      "oncontextlost",
      "oncontextmenu",
      "oncontextrestored",
      "oncuechange",
      "ondblclick",
      "ondrag",
      "ondragend",
      "ondragenter",
      "ondragleave",
      "ondragover",
      "ondragstart",
      "ondrop",
      "ondurationchange",
      "onemptied",
      "onended",
      "onerror",
      "onfocus",
      "onformdata",
      "oninput",
      "oninvalid",
      "onkeydown",
      "onkeypress",
      "onkeyup",
      "onload",
      "onloadeddata",
      "onloadedmetadata",
      "onloadstart",
      "onmousedown",
      "onmouseenter",
      "onmouseleave",
      "onmousemove",
      "onmouseout",
      "onmouseover",
      "onmouseup",
      "onmousewheel",
      "onpause",
      "onplay",
      "onplaying",
      "onprogress",
      "onratechange",
      "onreset",
      "onresize",
      "onscroll",
      "onscrollend",
      "onsecuritypolicyviolation",
      "onseeked",
      "onseeking",
      "onselect",
      "onslotchange",
      "onstalled",
      "onsubmit",
      "onsuspend",
      "ontimeupdate",
      "ontoggle",
      "onvolumechange",
      "onwaiting",
      "onwebkitanimationend",
      "onwebkitanimationiteration",
      "onwebkitanimationstart",
      "onwebkittransitionend",
      "onwheel",
      "onauxclick",
      "ongotpointercapture",
      "onlostpointercapture",
      "onpointerdown",
      "onpointermove",
      "onpointerup",
      "onpointercancel",
      "onpointerover",
      "onpointerout",
      "onpointerenter",
      "onpointerleave",
      "onselectstart",
      "onselectionchange",
      "onanimationend",
      "onanimationiteration",
      "onanimationstart",
      "ontransitionrun",
      "ontransitionstart",
      "ontransitionend",
      "ontransitioncancel",
      "onafterprint",
      "onbeforeprint",
      "onbeforeunload",
      "onhashchange",
      "onlanguagechange",
      "onmessage",
      "onmessageerror",
      "onoffline",
      "ononline",
      "onpagehide",
      "onpageshow",
      "onpopstate",
      "onrejectionhandled",
      "onstorage",
      "onunhandledrejection",
      "onunload",
      "isSecureContext",
      "crossOriginIsolated",
      "scheduler",
      "performance",
      "trustedTypes",
      "indexedDB",
      "localStorage",
      "sessionStorage",
      "alert",
      "atob",
      "blur",
      "btoa",
      "cancelAnimationFrame",
      "cancelIdleCallback",
      "captureEvents",
      "clearInterval",
      "clearTimeout",
      "close",
      "confirm",
      "createImageBitmap",
      "fetch",
      "find",
      "focus",
      "getComputedStyle",
      "getSelection",
      "matchMedia",
      "moveBy",
      "moveTo",
      "open",
      "postMessage",
      "print",
      "prompt",
      "queueMicrotask",
      "releaseEvents",
      "reportError",
      "requestAnimationFrame",
      "requestIdleCallback",
      "resizeBy",
      "resizeTo",
      "scroll",
      "scrollBy",
      "scrollTo",
      "setInterval",
      "setTimeout",
      "stop",
      "structuredClone",
      "webkitCancelAnimationFrame",
      "webkitRequestAnimationFrame",
      "chrome",
      "cookieStore",
      "ondevicemotion",
      "ondeviceorientation",
      "ondeviceorientationabsolute",
      "onpointerrawupdate",
      "caches",
      "documentPictureInPicture",
      "sharedStorage",
      "fetchLater",
      "getScreenDetails",
      "queryLocalFonts",
      "showDirectoryPicker",
      "showOpenFilePicker",
      "showSaveFilePicker",
      "originAgentCluster",
      "viewport",
      "onpageswap",
      "onpagereveal",
      "credentialless",
      "fence",
      "launchQueue",
      "speechSynthesis",
      "onscrollsnapchange",
      "onscrollsnapchanging",
      "ongamepadconnected",
      "ongamepaddisconnected",
      "webkitRequestFileSystem",
      "webkitResolveLocalFileSystemURL",
      "AppInit",
      "_epicEnableCookieGuard",
      "__tracking_base",
      "_sentryDebugIds",
      "_sentryDebugIdIdentifier",
      "SENTRY_RELEASE",
      "__axiosInstance",
      "__core-js_shared__",
      "core",
      "regeneratorRuntime",
      "__axiosInstanceCached",
      "IMask",
      "__STATSIG__",
      "__store",
      "__SENTRY__",
      "MotionHandoffIsComplete",
      "clearImmediate",
      "setImmediate",
      "_epicTrackingCookieDomainId",
      "_epicTrackingCountryCode",
      "_epicTracking",
      "a0_0x35f7",
      "a0_0x13b0",
      "talon",
      "hCaptchaLoaded",
      "hCaptchaReady",
      "Raven",
      "hcaptcha",
      "grecaptcha",
      "k",
      "i",
      "TEMPORARY",
      "PERSISTENT",
      "addEventListener",
      "dispatchEvent",
      "removeEventListener",
      "when"
    ]
  },
  "8": {
    "timezone_offset": -60,
    "format": {
      "calendar": "gregory",
      "day": "numeric",
      "locale": "de",
      "month": "numeric",
      "numbering_system": "latn",
      "time_zone": "Europe/Berlin",
      "year": "numeric"
    }
  },
  "9": {
    "sd_recurse": false
  },
  "10": {
    "version": "3.4.2",
    "visitor_id": "510ce0e6a2a490540b157f1af9319c96",
    "confidence": 0.6,
    "hashes": {
      "fonts": "cb8d075615d495f39c0fee44cb2bd348",
      "plugins": "7bf9267ddde7a33539244ab8ffe927d5",
      "audio": "81c423152c811da0c92dcbe04435dbfe",
      "canvas": "d0cac4e8853cb63c51eb727a03be6174",
      "screen": "6d4d6e93c094135d8e0a5b02390f74bb"
    }
  },
  "11": {
    "mousemove": [
      {
        "t": 2373.900000002235,
        "x": 1916,
        "y": 745
      },
      {
        "t": 2423.60000000149,
        "x": 1629,
        "y": 653
      },
      {
        "t": 2473.5,
        "x": 1362,
        "y": 545
      },
      {
        "t": 2523.60000000149,
        "x": 1227,
        "y": 480
      },
      {
        "t": 2551.60000000149,
        "x": 1214,
        "y": 468
      },
      {
        "t": 2633.699999999255,
        "x": 1214,
        "y": 467
      },
      {
        "t": 2686.5,
        "x": 1184,
        "y": 462
      },
      {
        "t": 2736.699999999255,
        "x": 1119,
        "y": 468
      },
      {
        "t": 2786.60000000149,
        "x": 1080,
        "y": 480
      },
      {
        "t": 2836.60000000149,
        "x": 1066,
        "y": 502
      },
      {
        "t": 2884.60000000149,
        "x": 1059,
        "y": 527
      },
      {
        "t": 2904.699999999255,
        "x": 1058,
        "y": 531
      },
      {
        "t": 2986.699999999255,
        "x": 1073,
        "y": 531
      },
      {
        "t": 3039.60000000149,
        "x": 1090,
        "y": 522
      },
      {
        "t": 3089.60000000149,
        "x": 1091,
        "y": 508
      },
      {
        "t": 3140.60000000149,
        "x": 1093,
        "y": 499
      },
      {
        "t": 3189.60000000149,
        "x": 1097,
        "y": 492
      },
      {
        "t": 3236.60000000149,
        "x": 1096,
        "y": 491
      },
      {
        "t": 3272.699999999255,
        "x": 1094,
        "y": 493
      },
      {
        "t": 3345.699999999255,
        "x": 1093,
        "y": 493
      },
      {
        "t": 3364.60000000149,
        "x": 1092,
        "y": 495
      },
      {
        "t": 3445.60000000149,
        "x": 1100,
        "y": 489
      },
      {
        "t": 3495.60000000149,
        "x": 1155,
        "y": 457
      },
      {
        "t": 3545.699999999255,
        "x": 1276,
        "y": 391
      },
      {
        "t": 3593.199999999255,
        "x": 1349,
        "y": 365
      },
      {
        "t": 3604.699999999255,
        "x": 1353,
        "y": 364
      },
      {
        "t": 3688.5,
        "x": 1353,
        "y": 364
      },
      {
        "t": 4394.900000002235,
        "x": 1442,
        "y": 776
      },
      {
        "t": 4442.699999999255,
        "x": 1441,
        "y": 774
      },
      {
        "t": 4496.60000000149,
        "x": 1434,
        "y": 764
      },
      {
        "t": 4498.699999999255,
        "x": 1433,
        "y": 764
      },
      {
        "t": 23562.300000000745,
        "x": 565,
        "y": 507
      },
      {
        "t": 23613.199999999255,
        "x": 462,
        "y": 525
      },
      {
        "t": 23662.199999999255,
        "x": 431,
        "y": 538
      },
      {
        "t": 23715.199999999255,
        "x": 440,
        "y": 547
      },
      {
        "t": 23764.10000000149,
        "x": 567,
        "y": 553
      },
      {
        "t": 24769.5,
        "x": 566,
        "y": 585
      },
      {
        "t": 24820.199999999255,
        "x": 459,
        "y": 579
      },
      {
        "t": 24870.199999999255,
        "x": 404,
        "y": 582
      },
      {
        "t": 24899.199999999255,
        "x": 393,
        "y": 587
      },
      {
        "t": 25205.300000000745,
        "x": 393,
        "y": 586
      },
      {
        "t": 25256.199999999255,
        "x": 416,
        "y": 566
      },
      {
        "t": 25295.199999999255,
        "x": 439,
        "y": 540
      },
      {
        "t": 25357.300000000745,
        "x": 420,
        "y": 570
      },
      {
        "t": 25406.400000002235,
        "x": 400,
        "y": 584
      },
      {
        "t": 25447.199999999255,
        "x": 399,
        "y": 586
      },
      {
        "t": 25506.199999999255,
        "x": 395,
        "y": 592
      },
      {
        "t": 25521.300000000745,
        "x": 394,
        "y": 593
      },
      {
        "t": 25711.199999999255,
        "x": 396,
        "y": 591
      },
      {
        "t": 25767.300000000745,
        "x": 417,
        "y": 579
      },
      {
        "t": 25817.199999999255,
        "x": 474,
        "y": 545
      },
      {
        "t": 25867.300000000745,
        "x": 564,
        "y": 499
      },
      {
        "t": 25868.199999999255,
        "x": 566,
        "y": 498
      },
      {
        "t": 43405.699999999255,
        "x": 567,
        "y": 521
      },
      {
        "t": 43455.800000000745,
        "x": 495,
        "y": 585
      },
      {
        "t": 43505.699999999255,
        "x": 441,
        "y": 638
      },
      {
        "t": 43555.800000000745,
        "x": 419,
        "y": 663
      },
      {
        "t": 43604.699999999255,
        "x": 404,
        "y": 687
      },
      {
        "t": 43656.699999999255,
        "x": 394,
        "y": 695
      },
      {
        "t": 43706.699999999255,
        "x": 388,
        "y": 705
      },
      {
        "t": 43714.699999999255,
        "x": 388,
        "y": 706
      },
      {
        "t": 43816.60000000149,
        "x": 388,
        "y": 706
      }
    ],
    "mousedown": [
      {
        "t": 3599.900000002235,
        "x": 1349,
        "y": 365
      },
      {
        "t": 25542.699999999255,
        "x": 394,
        "y": 593
      },
      {
        "t": 43713.900000002235,
        "x": 388,
        "y": 705
      }
    ],
    "mouseup": [
      {
        "t": 3687.800000000745,
        "x": 1353,
        "y": 364
      },
      {
        "t": 25620.199999999255,
        "x": 394,
        "y": 593
      },
      {
        "t": 43815.699999999255,
        "x": 388,
        "y": 706
      }
    ],
    "wheel": [],
    "touchstart": [],
    "touchend": [],
    "touchmove": [],
    "scroll": [],
    "keydown": [],
    "keyup": [],
    "resize": [
      {
        "t": 4505.699999999255,
        "w": 1920,
        "h": 1080
      }
    ],
    "paste": []
  },
  "12": {
    "caller_stack_trace": "Error\n    at https://talon-website-prod.ecosec.on.epicgames.com/talon_sdk.js:1:516667\n    at Object._0x9cbd8d [as execute] (https://talon-website-prod.ecosec.on.epicgames.com/talon_sdk.js:1:516842)\n    at Talon.updateIfNeeded (https://static-assets-prod.unrealengine.com/account-portal/static/assets/index-QoEJFRtM.js:599:37992)\n    at Captcha.updateIfNeeded (https://static-assets-prod.unrealengine.com/account-portal/static/assets/index-QoEJFRtM.js:599:40512)\n    at EmailRequestForm.<anonymous> (https://static-assets-prod.unrealengine.com/account-portal/static/assets/index-QoEJFRtM.js:599:53551)\n    at Generator.next (<anonymous>)\n    at https://static-assets-prod.unrealengine.com/account-portal/static/assets/index-QoEJFRtM.js:2:975\n    at new Promise (<anonymous>)\n    at br (https://static-assets-prod.unrealengine.com/account-portal/static/assets/index-QoEJFRtM.js:2:764)\n    at https://static-assets-prod.unrealengine.com/account-portal/static/assets/index-QoEJFRtM.js:599:53319"
  },
  "13": null,
  "14": false
}
```

## Example of encrypted fingerprint

```
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
```

## License

This project is licensed under the MIT License.

This project is for educational and research purposes only and is not affiliated
with, endorsed, or sponsored by any company or organization.
