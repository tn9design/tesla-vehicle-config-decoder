# Tesla Vehicle Config Decoder

This is an **unofficial** helper to generate Tesla image-compositor URLs for supported Model S, Model 3, and Model Y configurations. It lets you pick trim, paint, wheels, interior, view, and background, then builds a URL that you can use anywhere a direct image link is helpful, including a webpage or Home Assistant dashboard. It is a static web app that runs entirely in your browser with no login and no server-side code.

**Note:** This project is not affiliated with or endorsed by Tesla. “Tesla”, “Model S”, “Model 3”, and “Model Y” are trademarks of Tesla, Inc.

## Features

- Switch between supported Model S, Model 3, and Model Y configurations
- Choose year buckets where verified legacy Tesla compositor profiles are available
- Select trim, paint, wheels, interior, steering, and view with trim-scoped option lists
- Jump automatically to wheel or interior views when changing wheel or cabin-related options
- Add extra comma-separated option tokens for packages not surfaced in the dropdowns
- Generate Tesla compositor URLs with live image preview
- Copy the raw image URL or a Home Assistant YAML snippet
- Open a help modal with instructions for submitting unsupported Tesla config URLs

## Usage

This is a static HTML file. To run it locally:

1. Download the `index.html` file from this repository.
2. Open it in any modern web browser (Chrome, Firefox, Safari, Edge).
3. Choose your desired configuration; the app will update the URL and preview automatically.
4. Click `Copy URL` to copy the image URL or `Copy HA YAML` to copy a snippet for Home Assistant.

You can also host it as a GitHub Pages site, or on any static hosting, by uploading the file as-is and enabling your preferred static hosting flow.

### Home Assistant example

After generating a URL, the `Copy HA YAML` button gives you a ready-to-paste snippet. It looks like this:

```
 type: picture  
 image: "https://static-assets.tesla.com/configurator/compositor?context=design_studio_2&options=$MTS23,$PN02,$WS14,$IWC02&view=FRONT34&model=ms&size=1920&bkba_opt=2&crop=0,0,0,0&overlay=0"  
 tap_action:  
   action: url  
   url_path: "https://static-assets.tesla.com/configurator/compositor?context=design_studio_2&options=$MTS23,$PN02,$WS14,$IWC02&view=FRONT34&model=ms&size=1920&bkba_opt=2&crop=0,0,0,0&overlay=0"  
```

Paste this into your Lovelace dashboard YAML to display your car and allow tapping to open the image in a new tab.

## Option Code Reference

This section documents codes that are currently supported in the app or intentionally passed through for known Tesla configs. The goal is to keep this list limited to tokens that have been verified in Tesla's compositor URLs, not every community-documented option code.

Some entries are single tokens. Others are bundled combinations because Tesla only rendered them reliably together in testing, and the UI keeps those combinations intact.

<details>
<summary><strong>Model S</strong></summary>

### Modern Model S (`2024-2026`)

#### Model / Trim

| Code | Description |
| --- | --- |
| `$MTS22` | Dual Motor AWD |
| `$MTS23` | Plaid |

#### Paint

| Code | Description |
| --- | --- |
| `$PN01` | Stealth Grey |
| `$PPSW` | Pearl White Multi-Coat |
| `$PX02` | Diamond Black |
| `$PB00` | Frost Blue Metallic |
| `$PR01` | Ultra Red |
| `$PN02` | Lunar Silver |

#### Wheels

| Code | Description |
| --- | --- |
| `$WS93` | 19" Magnetite, Dual Motor |
| `$WS13` | 21" Velarium, Dual Motor |
| `$WS94` | 19" Magnetite, Plaid |
| `$WS14` | 21" Velarium, Plaid |

#### Interior

| Code | Description |
| --- | --- |
| `$IBE01` | All Black, Dual Motor |
| `$IWW01` | Black & White, Dual Motor |
| `$ICW01` | Cream, Dual Motor |
| `$IBC02` | All Black, Plaid |
| `$IWC02` | Black & White, Plaid |
| `$ICC02` | Cream, Plaid |

#### Steering

| Code | Description |
| --- | --- |
| `$ST06` | Standard Steering Wheel |
| `$ST1Y` | Yoke Steering |

### Legacy Model S (`2021-2023`)

#### Model / Trim

| Code | Description |
| --- | --- |
| `$MDLS` | Model S identifier used in legacy `v1/compositor` URLs |
| `$MTS13` | Dual Motor AWD |
| `$MTS14` | Plaid |

#### Paint

| Code | Description |
| --- | --- |
| `$PBSB` | Solid Black |
| `$PPSW` | Pearl White Multi-Coat |
| `$PPSB` | Deep Blue Metallic |
| `$PMNG` | Midnight Silver Metallic |
| `$PPMR` | Red Multi-Coat |

#### Wheels

| Code | Description |
| --- | --- |
| `$WS90` | 19" Tempest |
| `$WS11` | 21" Arachnid |

#### Interior

| Code | Description |
| --- | --- |
| `$IBE00` | All Black, wood trim |
| `$IWW00` | Black & White, wood trim |
| `$ICW00` | Cream, wood trim |
| `$IBC00` | All Black, carbon trim, Plaid |
| `$IWC00` | Black & White, carbon trim, Plaid |
| `$ICC00` | Cream, carbon trim, Plaid |

#### Steering

| Code | Description |
| --- | --- |
| `$ST0Y` | Yoke Steering |
| `$ST00` | Round Steering Wheel |

#### Extra pass-through codes

| Code | Description |
| --- | --- |
| `$APF2` | Autopilot hardware / FSD computer-related token, currently treated as pass-through metadata |
| `$APBS` | Autopilot package token, currently treated as pass-through metadata |
| `$SC04` | Supercharging-related token, currently treated as pass-through metadata |
| `$CPF1` | Decor/package token observed in legacy URLs, not currently verified as visually active |

</details>

<details>
<summary><strong>Model 3</strong></summary>

### Modern Model 3 (`2024-2026`)

#### Trim

| Code | Description |
| --- | --- |
| `$MT367` | Rear-Wheel Drive |
| `$MT369` | Rear-Wheel Drive (Premium) |
| `$MT370` | All-Wheel Drive (Premium) |
| `$MT371` | Performance (AWD) |

#### Paint

| Code | Description |
| --- | --- |
| `$PN01` | Stealth Grey |
| `$PPSW` | Pearl White Multi-Coat |
| `$PPSB` | Deep Blue Metallic |
| `$PX02` | Diamond Black |
| `$PR01` | Ultra Red |
| `$PN00` | Quicksilver |

#### Wheels

| Code | Description |
| --- | --- |
| `$W38C` | 18" Prismata |
| `$W39G` | 19" Nova |
| `$W38A` | 18" Prismata, premium trims |
| `$W30A` | 20" Warp |

#### Interior

| Code | Description |
| --- | --- |
| `$IBB4` | All Black, Rear-Wheel Drive |
| `$IPB2` | All Black, Rear-Wheel Drive (Premium) |
| `$IPW2` | Black & White, Rear-Wheel Drive (Premium) |
| `$IPB3` | All Black, All-Wheel Drive (Premium) |
| `$IPW3` | Black & White, All-Wheel Drive (Premium) |
| `$IPB4` | All Black, Performance |
| `$IPW4` | Black & White, Performance |

### Legacy Model 3 (`2018-2020`)

#### Trim

| Code | Description |
| --- | --- |
| `$MT301` | Standard Range Plus RWD |
| `$MT310` | Long Range AWD |
| `$MT311` | Performance AWD |

#### Paint

| Code | Description |
| --- | --- |
| `$PPSW` | Pearl White Multi-Coat |
| `$PBSB` | Solid Black |
| `$PMNG` | Midnight Silver Metallic |
| `$PPSB` | Deep Blue Metallic |
| `$PPMR` | Red Multi-Coat |
| `$PMSS` | Silver Metallic |

#### Wheels

| Code | Description |
| --- | --- |
| `$W38B` | 18" Aero |
| `$W39B` | 19" Sport |
| `$W32B,$SLR1` | 20" Sport, bundled with spoiler token in the app |
| `$W32D,$SLR1` | 20" Gray Sport, bundled with spoiler token in the app |

#### Interior

| Code | Description |
| --- | --- |
| `$IN3PB` | All Black |
| `$IN3PW,$PFP31` | Black & White, bundled with premium interior token in the app |

#### Other verified URL tokens

| Code | Description |
| --- | --- |
| `$PFP31` | Premium interior-related token used with legacy white interior |
| `$SLR1` | Spoiler token paired with legacy Performance wheel bundles |

</details>

<details>
<summary><strong>Model Y</strong></summary>

### Modern Model Y (`2025-2026`)

#### Trim

| Code | Description |
| --- | --- |
| `$MTY61` | Rear-Wheel Drive |
| `$MTY77` | All-Wheel Drive |
| `$MTY60` | Rear-Wheel Drive (Premium) |
| `$MTY48` | All-Wheel Drive (Premium) |
| `$MTY70` | Performance (AWD) |

#### Paint

| Code | Description |
| --- | --- |
| `$PN01` | Stealth Grey |
| `$PPSW` | Pearl White Multi-Coat |
| `$PPSB` | Deep Blue Metallic |
| `$PX02` | Diamond Black |
| `$PR01` | Ultra Red |
| `$PN00` | Quicksilver |

#### Wheels

| Code | Description |
| --- | --- |
| `$WY18P` | 18" Aperture |
| `$WY19P` | 19" Crossflow |
| `$WY21A` | 21" Arachnid 2.0 |

#### Interior

| Code | Description |
| --- | --- |
| `$IBB3` | All Black |
| `$IPB12` | All Black, premium trims |
| `$IPW12` | Black & White, premium trims |
| `$IPB14` | All Black, Performance |
| `$IPW14` | Black & White, Performance |

### Legacy Model Y (`2020-2024`)

#### Trim

| Code | Description |
| --- | --- |
| `$MTY09` | Long Range AWD |
| `$MTY12` | Performance AWD |

#### Paint

| Code | Description |
| --- | --- |
| `$PPSW` | Pearl White Multi-Coat |
| `$PBSB` | Solid Black |
| `$PMNG` | Midnight Silver Metallic |
| `$PPSB` | Deep Blue Metallic |
| `$PPMR` | Red Multi-Coat |

#### Wheels

| Code | Description |
| --- | --- |
| `$WY19B` | 19" Gemini |
| `$WY20P` | 20" Induction |
| `$WY21P` | 21" Uberturbine |

#### Interior

| Code | Description |
| --- | --- |
| `$INPB0` | All Black |
| `$INPW0` | Black & White |

</details>

### Notes

- Codes are only promoted into the UI after they have been checked against Tesla's compositor output.
- Some valid Tesla URLs include metadata or package tokens that do not appear to change the rendered image. Those may still be preserved in `Extra option codes`.
- Bundled code combinations such as `$W32B,$SLR1` or `$IN3PW,$PFP31` are documented that way because the app intentionally keeps those pairs together.

## License

This code is provided under the MIT License. See `LICENSE` for details. Use at your own risk and respect Tesla's terms of service when calling Tesla endpoints.
