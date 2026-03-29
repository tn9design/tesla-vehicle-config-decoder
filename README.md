# Tesla Vehicle Config Decoder  

This is an **unofficial** helper to generate Tesla’s image-compositor URLs for the Model S.  It lets you pick trim, paint, wheels, interior, view and background, then builds a URL that you can use anywhere (a webpage, a Home Assistant dashboard, etc.) to display your configured car. It’s a static web app that runs entirely in your browser – no login, no server-side code.  

**Note:** This project is not affiliated with or endorsed by Tesla. “Tesla” and “Model S” are trademarks of Tesla, Inc.  

## Features  

- Select trim (Dual Motor or Plaid)  
- Select paint, wheels and interior (with trim‑specific options)  
- Switch between modern visuals and legacy 2021-2023 `v1/compositor` visuals (Model S)  
- Choose camera angles: Front 3/4, Rear 3/4, Side profile, Rim close‑up, or Interior  
- Add extra comma-separated option tokens for older packages not surfaced in the dropdowns  
- Choose background: studio or transparent  
- Generate the URL for Tesla’s compositor endpoint  
- Live preview of the image  
- Copy the URL to your clipboard  
- Copy a Home Assistant YAML snippet with the image URL  
- Toggle studio/transparent URLs for dark/light use  
- Switch Model S between refresh visuals and 2021-2023 legacy `v1/compositor` visuals  
- Add extra Tesla option tokens for older builds that expose packages outside the dropdowns  

## Usage  

This is a static HTML file. To run it locally:  

1. Download the `index.html` file from this repository.  
2. Open it in any modern web browser (Chrome, Firefox, Safari, Edge).  
3. Choose your desired configuration; the app will update the URL and preview automatically.  
4. Click “Copy URL” to copy the image URL or “Copy HA YAML” to copy a snippet for Home Assistant.  

You can also host it as a GitHub Pages site (or on any static hosting) by uploading the file as-is and enabling Pages in your repository settings.  

### Home Assistant example  

After generating a URL, the “Copy HA YAML” button gives you a ready-to-paste snippet. It looks like this:  

```
 type: picture  
 image: "https://static-assets.tesla.com/configurator/compositor?context=design_studio_2&options=$MTS23,$PN02,$WS14,$IWC02&view=FRONT34&model=ms&size=1920&bkba_opt=2&crop=0,0,0,0&overlay=0"  
 tap_action:  
   action: url  
   url_path: "https://static-assets.tesla.com/configurator/compositor?context=design_studio_2&options=$MTS23,$PN02,$WS14,$IWC02&view=FRONT34&model=ms&size=1920&bkba_opt=2&crop=0,0,0,0&overlay=0"  
```

Paste this into your Lovelace dashboard YAML to display your car and allow tapping to open the image in a new tab.  

## Option Code Reference (Verified / In Progress)

The latest generation of Tesla vehicles uses new one‑letter/number option tokens in the configurator URL. These tokens map to specific trim, paint and feature choices. The following table documents the tokens observed so far. If you discover new codes, feel free to extend this table.

| Token    | Description                                                   |
| -------- | ------------------------------------------------------------- |
| `$MDLS`  | Vehicle model – Model S                                       |
| `$MTS13` | Trim – Dual Motor AWD (legacy 2021-2023 Model S visuals)      |
| `$MTS14` | Trim – Plaid AWD (legacy 2021-2023 Model S visuals)           |
| `$PBSB`  | Exterior colour – Solid Black                                 |
| `$WS90`  | Wheels – 19″ Tempest wheels                                   |
| `$WS11`  | Wheels – 21″ Arachnid wheels                                  |
| `$APF2`  | Autopilot hardware 3.0 / Full Self‑Driving computer           |
| `$APBS`  | Autopilot software base package                               |
| `$SC04`  | Paid supercharging (no free credits)                          |
| `$IBE00` | Legacy interior – All Black with wood trim                    |
| `$IWW00` | Legacy interior – Black & White with wood trim                |
| `$ICW00` | Legacy interior – Cream with wood trim                        |
| `$IBC00` | Legacy Plaid interior – All Black with carbon trim            |
| `$IWC00` | Legacy Plaid interior – Black & White with carbon trim        |
| `$ICC00` | Legacy Plaid interior – Cream with carbon trim                |
| `$ST0Y`  | Steering – Yoke steering wheel                                |
| `$CPF1`  | Candidate decor/package token, not verified as visually active|

Verified findings from compositor testing:

- Legacy Plaid (`$MTS14`) supports distinct carbon-trim interior tokens (`$IBC00`, `$IWC00`, `$ICC00`) in `STUD_INTERIOR` renders.
- Legacy spoiler candidates (`$SLR0`, `$SLR1`) did not produce a visible change in tested rear renders.
- Legacy brake caliper candidates (`$BC0B`, `$BC0R`) did not produce a visible change in tested wheel close-up renders.
- Package tokens like `$APF2`, `$APBS`, and `$SC04` appear to be pass-through metadata for our use case rather than visible render toggles.

*Note:* Many Tesla codes are still being decoded by the community, and the unofficial option-code list is only a hint source. We only promote tokens into the UI after confirming they affect the compositor output.


## License  

This code is provided under the MIT License (see `LICENSE` for details).  Use at your own risk and respect Tesla’s terms of service when calling their endpoints.
