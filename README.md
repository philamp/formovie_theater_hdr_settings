# Formovie Theater Calibration

My calibration values for the Formovie Theater projector, which is hard to calibrate in HDR for some reason.
I'm open to any contribution to improve these settings which I think are not yet optimal but gives good results. 
Initially this is based on : https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm.

> [!CAUTION]
> Keep in mind that :
> - all units are a little bit different and might need different calibration.
> - I'm projecting on a Vividstorm 92" CLR screen with a 0.6 gain.

> [!TIP]
> To test between different sets of values, you can switch between "user" and "standard" presets.

# 1/ HDR or LLDV HDR (BT2020)

## Main image
-- |  value  
----- | ----
Brightness | 48
Contrast   | 83 *
Saturation | 32
Hue        | 0
Gamma      | ``middle`` !

> [!TIP]
> \* This contrast value has to be adjusted :
> - On Pure HDR10 it's impossible to have a fixed value : you have to roughly find the max value that does not crush bright lights for each movie : it can be between 50 and 80. Maybe due to bad tone-mapping implementation (or rather HDR10 sources specified with MDL/MaxCLL way higher than any max pixel luminosity in the actual data).
> - On LLDV content (output as HDR10, see https://www.hdfury.com/enjoy-dynamic-dv-content-from-lldv-source-on-any-hdr10-display/) you can keep a fixed value once you've found the max value that does not crush bright lights (+ 2 points below to have little margin)
>   - My LLDV equivalent settings are :
>     - BT2020 primaries
>     - ~0.035 nits for minlum (maybe too low for 92" projection size)
>     - ~280 nits for maxlum (maybe too high, it's absolutely allright to go down to 100 nits if you have a big screen thus less nits)

## Color temperature
--  | value
---- | ----
R | -2
G | -12
B | -28

> might be "cooler" than projector central's advised one (d65) but it's a compromise to keep good gamut coverage.

## Color management

-- | HUE | SATURATION | BRIGHTNESS
---- | ---- | ---- | ----
R | 53 | 53 | 70 
G | 41 | 54 | 70 
B | 51 | 50 | 79 
C | 57 | 46 | 76 
M | 40 | 59 | 73 
Y | 60 | 42 | 70 
FT | 48 | 47 | 65 

--  | OFFSET |  GAIN
---- | ---- | ----
R | 48 | 48
G | 50 | 44
B | 50 | 40

> - HUE settings are the same as https//www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm .
> - BRIGHTNESS Values are set around roughly 70 with some adjustements made from visual feedback, I think those values are not yet optimal. You can test having all set to 50.
> - SATURATION are based on projector central but with lower values for R, G and FT , to avoid unatural skin tones (and the result seems close to natural to me).
> - For Magenta I'm not sure such a high value is great.


# 2/ SDR (BT709 or BT2020)
For SDR Calibration:
- I think https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm settings are very good.
- ``Color space`` must be set to ``on`` in ``Advanced video``.

# 3/ General

## Advanced video
--  | value
---- | ----
Hdmi rgb range | ``auto``
color space | ``auto`` (HDR) ; ``on`` (SDR) 
Di film mode | ``auto``
Decounter | ``off`` or ``low``
Everything else | ``off`` !

> - ``Flesh tone`` set to ``on`` could help in HDR if you still find flesh tone to be too saturated, but I don't advise it.
> - On poor SDR8 content these settings can be great :
>   - ``De-counter`` set to ``middle`` to mitigate color banding artefacts. 
>   - ``MPEG NR`` to mitigate compression artefacts.
> - ``DNR`` gives smearing effects sometimes. I think it must be avoided.  

## About Contrast
This projector has a *very* good 'potential' contrast. It means that to achieve its full potential, the digital maximum brightness value must fit 'just well' within physical capabilities of the projector.
- In SDR, the 52/40 (brightness/contrast) values will fit well and source material is always fitting well because SDR is easier to deal with.
- In HDR, as advised in 'Main image', contrast slider must be visually tuned because source material is not always 'fitting well' in terms of actual data and HDR metadata used by the tone-mapping.
- In native Dolby Vision mode, Formovie has opted to cap the max brithness to roughly half of the projector/s capabilities. It's maybe to ensure consistant color calibration across luminosity although they recently said they would release a firmware around june 2024 to fix that. In the meantime, the LLDV method is a "power user" solution to break that limit.

> [!CAUTION]
> Online reviews are measuring contrast without taking that into account and they come up with contrast values that are lower in HDR mode than in SDR.

> [!TIP]
> - Tone-mapping in SDR will only fix this issue marginally, but is also a good solution if your player device has good HDR to SDR tone-mapping, especially if your screen max luminosity is around 100 nits (as 100 nits value is used for the HDR to SDR tone-mapping).
> - ``Advanced video`` > ``Adaptive luma control`` set to ``middle`` (other values are suboptimal IMHO) can be great in SDR and can help in pure HDR too, but it's also matter of taste and it's somewhat breaking the director's intent.

## 11 points white balance correction
I found correction to be very subtle but great anyway : https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm .

# 4/ Resources
- https://lightillusion.com/what_is_hdr.html - has some very good points
- https://www.projectorscreen.com/projector-screen-calculators - Good to know therocial nits projected from you screen depending on several parameters and your viewing distance (No need to have a huge screen if you don't have enough step back in the room)
- https://confit.atlas.jp/guide/event-img/idw2020/PRJ5-02/public/pdf_archive?type=in - if you're curious about ALPD 4.0 technology used in this projector.
- https://avdisco.com/t/why-it-is-so-hard-to-calibrate-hdr-on-a-projector-and-more/248 - could be interesting, I'm not sure to agree on everything, but IMHO.
- Reviews:
  - https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm
  - https://www.projectorscreen.com/blog/2023-laser-tv-showdown-ultra-short-throw-projector-shootout
  - https://www.projectorscreen.com/blog/ForMovie-Theater-Global-UST-Projector-Review-Fengmi-T1-Global
  - https://www.projectorscreen.com/blog/How-to-Make-the-Formovie-Theater-Look-its-Best-Settings-Tips
