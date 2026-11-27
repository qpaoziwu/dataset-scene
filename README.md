# Synthetic dataset scene

Interactive case study for [richardhui.com/dataset](https://www.richardhui.com/dataset/): a tabletop scene from a multi-view 3D reconstruction spec, rendered in real time (Babylon.js) or path traced (three-gpu-pathtracer), with depth, normal, semantic and instance maps and the camera numbers saved for every view. An experimental synthetic skybox lights the scene from a real place, date and time, using published solar and daylight models or measured hourly weather.

`assets/` holds what the page loads: the iPhone model, measured-material lookup tables (Physically Based, CC0), texture thumbnails and Babylon's blue-noise texture (CC0). Textures and HDRIs load from Poly Haven's CDN (CC0).

## Model credits

- "Metal Mug Holder" by Mopra (https://sketchfab.com/3d-models/metal-mug-holder-34dfc5259e104e108c40c9e891b16f7b), CC-BY-4.0: split into a stand and six separate mugs, textures resized.
- "Apple Vision Pro" by Sketcher (https://sketchfab.com/3d-models/apple-vision-pro-d225809b5c8149bc9e866ad920cdba83), CC-BY-4.0: simplified, textures resized to 512 px WebP.
- Apple iPhone 18 Pro Max (Burgundy, 2026), https://sketchfab.com/3d-models/apple-iphone-18-pro-max-burgundy-2026-604acc18b5d5455d820a16359b45b003, licence as stated on the model page.

## Synthetic skybox (experimental)

- Sun position: NOAA Solar Calculator equations (after Meeus) with NOAA refraction. Checked against NREL SPA (pvlib): within 0.013° of elevation, 0.041° of azimuth over 400 random cases.
- Clear-sky irradiance: Ineichen & Perez 2002, Kasten & Young 1989 air mass, Spencer 1971 Earth–Sun distance; Linke turbidity from aerosol depth and water (Bird & Hulstrom 1980, Kasten 1996, Ineichen 2008). Matches pvlib's `ineichen` exactly.
- Sky shape: CIE standard general sky type 12 (ISO 15469:2004) for clear skies; Perez, Seals & Michalsky 1993 all-weather sky for measured weather, with coefficients and bin rules from Radiance `gendaylit.c`.
- Colour: SPCTRL2 (Bird & Riordan 1986) direct and diffuse spectra, integrated with the CIE 1931 2° observer.
- Weather data by [Open-Meteo.com](https://open-meteo.com/) (CC BY 4.0): hourly direct normal and diffuse irradiance and cloud cover (ERA5 archive or forecast models), and CAMS aerosol depth.
- Limits: hourly means, cloud amount but not cloud positions, daylight only, uniform 20% ground.
