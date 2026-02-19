# Tesla Vehicle Config Decoder  

This is an **unofficial** helper to generate Tesla’s image-compositor URLs for the Model S.  It lets you pick trim, paint, wheels, interior, view and background, then builds a URL that you can use anywhere (a webpage, a Home Assistant dashboard, etc.) to display your configured car. It’s a static web app that runs entirely in your browser – no login, no server-side code.  

**Note:** This project is not affiliated with or endorsed by Tesla. “Tesla” and “Model S” are trademarks of Tesla, Inc.  

## Features  

- Select trim (Dual Motor or Plaid)  
- Select paint, wheels and interior (with trim‑specific options)  
- Choose camera angles: Front 3/4, Rear 3/4, Side profile, Rim close‑up, or Interior  
- Choose background: studio or transparent  
- Generate the URL for Tesla’s compositor endpoint  
- Live preview of the image  
- Copy the URL to your clipboard  
- Copy a Home Assistant YAML snippet with the image URL  
- Toggle studio/transparent URLs for dark/light use  

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

## Option Code Reference (2021+ Model S)

The latest generation of Tesla vehicles uses new one‑letter/number option tokens in the configurator URL. These tokens map to specific trim, paint and feature choices. The following table documents the tokens observed so far. If you discover new codes, feel free to extend this table.

| Token    | Description                                                   |
| -------- | ------------------------------------------------------------- |
| `$MDLS`  | Vehicle model – Model S                                       |
| `$MTS13` | Trim – Dual‑motor or Plaid (2021+ Model S refresh)            |
| `$PBSB`  | Exterior colour – Solid Black                                 |
| `$WS11`  | Wheels – 21″ Arachnid wheels                                  |
| `$APF2`  | Autopilot hardware 3.0 / Full Self‑Driving computer           |
| `$APBS`  | Autopilot software base package                               |
| `$SC04`  | Paid supercharging (no free credits)                          |
| `$CPF1`  | Interior décor – Carbon‑fibre trim                            |
| `$IWW00` | Interior colour – All‑black premium interior                  |
| `$ST0Y`  | Steering – Yoke steering wheel (2021+ Model S)                |

*Note:* Many of these codes are still being decoded by the community. Values labelled here are based on observed builds and may change over time.


## License  

This code is provided under the MIT License (see `LICENSE` for details).  Use at your own risk and respect Tesla’s terms of service when calling their endpoints.
