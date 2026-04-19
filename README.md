# Tesla Image Configurator

An unofficial static web app for generating Tesla image-compositor URLs for supported Model S, Model X, Model 3, and Model Y configurations.

The app lets you choose a model, year bucket, trim, paint, wheels, interior, steering, and view, then builds a direct Tesla compositor URL with a live preview. It is designed for owners who want a stable image URL for dashboards, automations, documentation, or personal use without needing to decode Tesla option tokens by hand.

Live configurator: [tn9design.github.io/tesla-vehicle-config-decoder](http://tn9design.github.io/tesla-vehicle-config-decoder/)

This project is not affiliated with or endorsed by Tesla. “Tesla”, “Model S”, “Model 3”, and “Model Y” are trademarks of Tesla, Inc.

## Project status

- Static single-file app with no backend
- Supports modern and verified legacy Tesla compositor profiles where testing confirmed the renders
- Focuses on real renderable combinations, not a speculative catalog of every community-known option code

## Features

- Supports Model S, Model X, Model 3, and Model Y
- Includes verified year buckets for legacy compositor profiles
- Uses trim-scoped paint, wheel, and interior option sets
- Automatically switches to wheel or interior views when those selections change
- Supports steering options on Model S, including legacy exterior-compatible steering tokens
- Generates direct Tesla compositor image URLs with live preview
- Copies raw Tesla compositor URLs and opens the rendered image directly
- Includes a help flow for submitting unsupported Tesla config URLs

## Quick start

### Use the hosted app

Open the live configurator:

[http://tn9design.github.io/tesla-vehicle-config-decoder/](http://tn9design.github.io/tesla-vehicle-config-decoder/)

### Run locally

1. Clone or download this repository.
2. Open [`index.html`](index.html) in any modern browser.
3. Choose a supported model and year profile.
4. Adjust the configuration until the preview matches your car.
5. Copy the generated URL or open the image directly.

Because the app is fully static, there is no build step and no dependency installation.

## How it works

Tesla exposes public image compositor endpoints that accept vehicle option codes in the query string. This project maps verified option-code combinations into a friendlier interface and assembles the correct URL format for the active model profile.

The app currently uses both:

- `https://static-assets.tesla.com/configurator/compositor`
- `https://static-assets.tesla.com/v1/compositor/`

Which endpoint is used depends on the selected vehicle profile.

## Supported profiles

Only profiles that were checked against Tesla's live compositor are exposed in the UI.

| Model | Year label in app | Endpoint family | Notes |
| --- | --- | --- | --- |
| Model S | `2024-2026` | `configurator/compositor` | Current/modern profile |
| Model S | `2021-2023` | `v1/compositor` | Legacy refresh-era profile with verified Plaid carbon interior variants |
| Model X | `2025-2026` | `configurator/compositor` | Current/modern profile with trim-scoped seating-layout control |
| Model X | `2021-2024` | `v1/compositor` | Legacy refresh-era profile with seating-layout control |
| Model 3 | `2024-2026` | `configurator/compositor` | Current/modern profile |
| Model 3 | `2021-2023` | `v1/compositor` | Legacy refresh-era profile, currently verified for Performance AWD only |
| Model 3 | `2018-2020` | `configurator/compositor` | Verified legacy profile using older view names |
| Model Y | `2025-2026` | `configurator/compositor` | Current/modern profile |
| Model Y | `2020-2024` | `v1/compositor` | Verified legacy profile |

## What is intentionally conservative

This project does not try to expose every Tesla token found on the internet.

- Tokens are added to the UI only after the compositor actually renders them cleanly.
- Some Tesla URLs include package or metadata tokens that do not appear to change the rendered image. Those are not promoted into first-class controls unless they prove visually meaningful.
- Some options are documented as bundled combinations because Tesla only rendered them reliably together in testing.

That conservative approach is deliberate. It keeps the app from generating misleading or broken URLs.

## Missing options and unsupported vehicles

If your exact vehicle options are not shown in the app:

1. Open the live configurator and click the missing-options help link near the bottom of the left column.
2. Copy the Tesla image/config URL from your Tesla account or pre-owned inventory image.
3. Open a GitHub issue and paste the full URL along with your model, year, trim, and any details that matter.

The app includes a built-in issue template flow for this.

## Repository layout

| File | Purpose |
| --- | --- |
| [`index.html`](index.html) | Entire app: markup, styles, data, and JavaScript logic |
| [`README.md`](README.md) | Project documentation |
| [`LICENSE`](LICENSE) | MIT license |

## Option Code Reference

This section documents codes that are currently supported in the app or intentionally preserved for known Tesla configs. It is not meant to be an exhaustive Tesla option-code database.

Some entries are single tokens. Others are bundled combinations because Tesla only rendered them reliably together in testing, and the UI preserves those combinations.

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
<summary><strong>Model X</strong></summary>

### Modern Model X (`2025-2026`)

#### Trim

| Code | Description |
| --- | --- |
| `$MDLX` | Model X identifier used in current compositor URLs |
| `$MTX22` | All-Wheel Drive |
| `$MTX23` | Plaid |

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
| `$WX02` | 20" Perihelix |
| `$WX23` | 22" Machina |

#### Interior

| Code | Description |
| --- | --- |
| `$IBE01` | All Black - Ebony |
| `$IWW01` | Black & White - Walnut |
| `$ICW01` | Cream - Walnut |
| `$IBC02` | All Black - Carbon |
| `$IWC02` | Black & White - Carbon |
| `$ICC02` | Cream - Carbon |

#### Seating

| Code | Description |
| --- | --- |
| `$STY5S` | Five Seat |
| `$SR04` | Six Seat |
| `$STY7S` | Seven Seat |

Current UI note:

- All-Wheel Drive exposes five-, six-, and seven-seat layouts.
- Plaid is currently restricted to six-seat layout.
- Current `22" Machina` is verified as `$WX23`.

#### Steering

| Code | Description |
| --- | --- |
| `$ST06` | Steering Wheel |
| `$ST1Y` | Yoke Steering |

### Legacy Model X (`2021-2024`)

#### Model / Trim

| Code | Description |
| --- | --- |
| `$MDLX` | Model X identifier used in legacy `v1/compositor` URLs |
| `$MTX10` | Long Range AWD |
| `$MTX14` | Plaid |

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
| `$WX00` | 20" Cyberstream |
| `$WX20` | 22" Turbine |

#### Interior

| Code | Description |
| --- | --- |
| `$IBE00` | All Black, Long Range |
| `$IWW00` | Black & White, Long Range |
| `$IBC00` | All Black, Plaid |
| `$IWC00` | Black & White, Plaid |

#### Seating

| Code | Description |
| --- | --- |
| `$STY5S` | Five Seat |
| `$SR04` | Six Seat |
| `$STY7S` | Seven Seat |

#### Steering

| Code | Description |
| --- | --- |
| `$ST03` | Round Steering Wheel |
| `$ST0Y` | Yoke Steering |

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

### Legacy Model 3 (`2021-2023`)

Current UI note:

- Currently verified for `Performance AWD` only. Additional owner URLs are still needed for other trims and wheel sets.
- The app preserves the full verified legacy package bundle for this profile because the `STUD_WHEEL` render falls back without it.

#### Trim

| Code | Description |
| --- | --- |
| `$MT317` | Performance AWD |

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
| `$W33D` | 20" Uberturbine |

#### Interior

| Code | Description |
| --- | --- |
| `$IPB1` | All Black |
| `$IPW1` | Black & White |

#### Other verified URL tokens

| Code | Description |
| --- | --- |
| `$MDL3` | Model 3 identifier used in legacy `v1/compositor` URLs |
| `$DV4W` | Legacy Performance-related token bundled with the verified trim in the app |
| `$SLR1` | Spoiler token paired with the verified legacy Performance wheel bundle |

#### Extra pass-through codes

| Code | Description |
| --- | --- |
| `$APBS` | Verified owner-URL token currently preserved with the legacy Performance profile |
| `$BC3R` | Verified owner-URL token currently preserved with the legacy Performance profile |
| `$PRM31` | Verified owner-URL token currently preserved with the legacy Performance profile |
| `$SC04` | Verified owner-URL token currently preserved with the legacy Performance profile |
| `$PL31` | Verified owner-URL token currently preserved with the legacy Performance profile |
| `$SPT31` | Verified owner-URL token currently preserved with the legacy Performance profile |
| `$CPF1` | Verified owner-URL token currently preserved with the legacy Performance profile |
| `$RSF1` | Verified owner-URL token currently preserved with the legacy Performance profile |
| `$CW03` | Verified owner-URL token currently preserved with the legacy Performance profile |

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

## Limitations

- Tesla can change or rate-limit its image endpoints at any time.
- Some real Tesla build codes do not appear to affect rendered images.
- Not every historical Tesla variant is supported yet.
- Older unsupported vehicles may require new year buckets rather than a few extra tokens.

## Contributing

Issues and pull requests are welcome, especially when they include:

- a real Tesla compositor or inventory image URL
- the exact model and approximate year
- the expected trim, wheels, paint, and interior
- a note about what the app currently gets wrong

## License

This project is released under the MIT License. See [`LICENSE`](LICENSE) for details.
