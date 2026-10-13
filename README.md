# <img src="logo.svg" width="32" height="32" valign="middle"> PS Store Avatar Adder

### Modified version of [yungtry/psn-avatar-unlocker](https://github.com/yungtry/psn-avatar-unlocker) with HK/JP/US store support.

A Tampermonkey userscript to add classic PS3/PS4 avatars to your PlayStation Store cart, including legacy items that are no longer listed in the web store.

<img src="screenshots/main.png" width="480" alt="PS Store Avatar Adder Panel">

[![Get Tampermonkey](https://img.shields.io/badge/Tampermonkey-Get%20Extension-008080?style=for-the-badge&logo=tampermonkey&logoColor=white)](https://www.tampermonkey.net/)
[![Direct Install](https://img.shields.io/badge/Direct%20Install-Raw%20Script-0072ce?style=for-the-badge&logo=github&logoColor=white)](https://raw.githubusercontent.com/cyguo11/ps-avatar-unlocker-hk-jp-us/main/ps3-avatar-adder-hk-jp-us.user.js)

## Installation

1. Install the [Tampermonkey](https://www.tampermonkey.net/) extension for your web browser.
2. Click [here](https://raw.githubusercontent.com/cyguo11/ps-avatar-unlocker-hk-jp-us/main/ps3-avatar-adder-hk-jp-us.user.js) to install the script.
3. Visit the [PlayStation Store](https://store.playstation.com/) and make sure you are logged in.

## Tutorial

Follow these steps to use the script:

1. Click the circular controller symbols button in the bottom left corner of the PlayStation Store page to open the panel.

   <br>
   <img src="screenshots/1.png" width="380" alt="PS Store Avatar Adder Panel">
   <br>

2. **Capture the API Hash**: The script requires a session-specific API hash to make requests. To capture it, simply add any standard item (such as a game [preorders do not work]) to your cart using the regular store buttons on the page. The status indicator in the panel will turn green and display the captured hash.
3. Remove the game from the cart
4. Paste the Avatar Content ID (for example, `EP0082-CUSA02487_00-FFXIVPIXAVATAR00`) into the input field.
5. Select your store region (HK / JP / US). The language is filled in automatically, and your PSN account must belong to the same region.
6. Click **Add to Cart**.
7. Check your official cart on the website to verify and complete the checkout.
8. Repeat step 4 for the next avatar.

*Note: You can delete the captured hash at any time in the Advanced settings section to recapture it.*

## Troubleshooting (Manual Hash)

If the automatic capture does not trigger:

1. Press `F12` and open the **Network** tab, filtered by **Fetch/XHR**.
2. Add any item to the cart on the store page.
3. Search for a network request named `op`.
4. Inspect the Request Payload or Body of the `op` request to find `sha256Hash` (a 64-character string).
5. Copy it, expand the **Advanced (Hash)** section in the script panel, paste the hash, and click **Save hash**.

## Browser & Manager Compatibility

| Environment | Status | Notes |
| --- | --- | --- |
| Chrome/Edge + Tampermonkey | ✅ Full | GM_xmlhttpRequest backend; hash and settings persist across sessions. |
| Firefox + Tampermonkey | ✅ Full | Same as above. |
| Firefox + Violentmonkey | ✅ Full | GM_xmlhttpRequest backend. |
| Firefox + Greasemonkey 4 | ✅ Supported | Uses the async `GM.xmlHttpRequest` / `GM.setValue` APIs. Full-page intercepts may be slightly less complete on this engine — use the manual hash flow if needed. |
| Safari + Userscripts app | ⚠️ Partial | No GM storage or cross-origin request APIs: the cart request is sent via the page's own `fetch()` (session-bound), and the captured hash/settings last only for the current tab session. |

Notes for limited environments:

- On Safari, use the same **Add any product to cart** capture flow — the hash capture works, but settings do not survive a page reload.
- On Greasemonkey 4, values persist, but if automatic capture misses the hash, use the [manual hash flow](#troubleshooting-manual-hash).

## Finding Avatar Content IDs

- **PSPrices (recommended)**: Open the [PSPrices avatar catalogue](https://psprices.com/region-hk/collection/avatars) for your region (replace `region-hk` with `region-jp` or `region-us`), open an avatar page, view the page source (`Cmd+Option+U` on Mac, `Ctrl+U` on Windows) and search for `"sku"`. The value in quotes is the Content ID. The same steps are shown in the panel under **如何使用？** (How to use).
- **Product URLs**: Look at web URLs of legacy PlayStation Store pages where the Content ID is part of the link.
- **Databases**: Use third-party community databases like [SerialStation](https://serialstation.com/), [PSNA](https://psna.online/EDAT-FILES) or [PSDeals](https://psdeals.net/) to lookup Content IDs by game name.

## Changes in this fork

- Region list limited to HK / JP / US, with the language set automatically from the region.
- Tries the correct SKU suffix for each store (`-H001` for HK, `-J001` for JP, `-U001` for US); the original only tried the EU `-E001` suffixes, so every HK item failed with `SKU not found`.
- Built-in usage guide in the panel.

## License

This project is licensed under the PolyForm Noncommercial License 1.0.0. Under this license, you are free to run, copy, modify, and distribute the script for noncommercial purposes, but any commercial use or distribution for sale is prohibited. See the [LICENSE](LICENSE) file for the full text.

Required Notice: Copyright 2026 yungtry (https://github.com/yungtry/psn-avatar-unlocker)
