# Formovie Theater Calibration

My calibration values for the Formovie Theater projector, which is hard to calibrate.
I'm open to any contribution to improve these settings which I think are not yet optimal but gives good results. 
Initially this is based on https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm.

> [!CAUTION]
> Keep in mind that :
> - all units are a little bit different and might need different calibration.
> - I'm projecting on a Vividstorm 92" CLR screen with a 0.6 gain.

# 1/ HDR or LLDV HDR (BT2020)

## Main image settings
-- |  value  
----- | ----
Brightness | 48
Contrast   | 83 *
Saturation | 32
Hue        | 0
Gamma      | ``middle`` !

> [!TIP]
> \* This contrast value has to be adjusted:
> - On Pure HDR10 it's impossible to have a fixed value : you have to roughly find the max value that does not crush bright lights for each movie : it can be between 50 and 80. Maybe due to bad tone-mapping implementation (or rather HDR10 sources specified with MDL/MaxCLL way higher than any max pixel luminosity in the actual data).
> - On LLDV content (output as HDR10, see https://www.hdfury.com/enjoy-dynamic-dv-content-from-lldv-source-on-any-hdr10-display/) you can keep a fixed value once you've found the max value that does not crush bright lights (+ 2 points below to have little margin)
>   - My LLDV equivalent settings are :
>     - BT2020 primaries
>     - ~0.035 nits for minlum (maybe too low)
>     - ~280 nits for maxlum (it's absolutely allright to go down to 100 nits if you have a big screen thus less nits)

## Color temperature
--  | value
---- | ----
R | -2
G | -12
B | -28

> (might be "cooler" than projector central's advised one (d65) but it's a compromise to keep good gamut coverage)

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

> - HUE settings are the same as https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm
> - BRIGHTNESS Values are set around roughly 70 with some adjustements made from visual feedback, I think those values are not yet optimal :/
> - SATURATION are based on projector central but with lower values for R, G and FT (and for magenta I'm not sure such a high value is great), to avoid unatural skin tones (and the result seems close to natural to me)


# 2/ SDR (BT709 or BT2020)
For SDR Calibration:
- I think https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm settings are very good.
- Color space must be set to ON in Advanced video settings

# 3/ General

## Advanced video

--  | value
---- | ----
Hdmi rgb range | ``auto``
color space | ``auto`` 
Di film mode | ``auto`` (HDR) ; ``on`` (SDR)
Decounter | ``off`` or ``low``
Everything else | ``off`` !

> Flesh tone ON could help in HDR if you still find flesh tone to be to saturated, but I don't advise it.
> Decounter ``middle`` is great on poor SDR8 content to create gradients from color banding artefacts.

## Contrast management
Note that adaptive luma control to "middle" (other values than 'middle' are suboptimal IMHO) can be great in SDR and can help in pure HDR too (especially with this contrast adjustement issue), but it's also matter of taste.

## 11 Point White Balance Correction
I found effect to be very subtle but I think https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm calibration on that matter is good.


