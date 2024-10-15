> [!TIP]
> - TLDR:
>   - In HDR mode (with brightness near 50), The projector *seems* to be configured to reach peak physical luminance at maxnits=500|maxcontrast=50, so it means you should not configure LLDV maxlum to less than 250 nits, otherwise you won't be able to reach peak brightness, because ramping up the contrast cursor stops at 100.
>   - [Projector Central](https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm) settings are mostly good for HUE but:
>     - CMS BRIGHTNESS settings are bad IMHO.
>     - They did not care to adjust RED both in GAIN and COLOR TEMPERATURE to avoid pink/purple noise on bright yellow lights.
>     - CMS GAIN seems to have very similar effect to COLOR TEMPERATURE, Thus I set GAIN to be neutral and only impacted COLOR TEMPERATURE
>     - CMS SATURATION settings are way too high in RED, GREEN, MAGENTA and FT, IMHO.
>   - Things I'm not getting (please explain to me):
>     - I don't know which GAMMA setting should be theorically set and I don't understand why this settings exists in HDR mode.
>     - Not sure that ``Adaptive luma control`` is not itself a tone-mapping algorithm.

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
Contrast   | 83 
Saturation | 32
Hue        | 0
**Gamma**      | ``middle`` !

> [!TIP]
> \* This contrast value has to be adjusted :
> - On Pure HDR10 it's impossible to have a fixed value : you have to roughly find the max value that does not crush bright lights for each movie : it can be between 50 and 80. Maybe due to bad tone-mapping implementation (or rather HDR10 sources specified with MDL/MaxCLL way higher than any max pixel luminosity in the actual data).
> - On LLDV content (output as HDR10, see https://www.hdfury.com/enjoy-dynamic-dv-content-from-lldv-source-on-any-hdr10-display/) you can keep a fixed value once you've found the max value that does not crush bright lights (+ 2 to 4 points below to have little margin)
>   - My LLDV equivalent settings are :
>     - BT2020 primaries
>     - ~0.035 nits for minlum (maybe too low for 92" projection size)
>     - ~280 nits for maxlum (maybe too high, ~~it's absolutely allright to go down to 100 nits if you have a big screen thus less nits~~ EDIT : Totally WRONG because of peak lum management in the unit, see explanations below)
>     - HDR10 metadata override : ``87:01:1a:5c:02:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00``
>    
> - *NEW: The CPM Coreelec build with compatible device can do the LLDV trick as well ! : https://discourse.coreelec.org/t/help-support-cpm-build/52613/223*

### About Contrast vs. HDR management

>  To understand this part please note that the CONTRAST setting impacts the peak brightness because it's like this transfer function : ``output_brightness = input_brightness * contrast_value``
> while brightness is basically ``output_brightness = input_brightness + brightness_value``
> - LLDV = Low Latency Dolby Vision : https://www.avsforum.com/threads/alternative-devices-for-enabling-lldv-please-read-posts-1-2.3254266/

This projector has a *very* good 'potential' contrast. It means that to achieve its full potential, the digital maximum brightness value must fit 'just well' within physical capabilities of the projector.
- In SDR, the 52/40 (brightness/contrast) values will fit well and source material is always fitting well because SDR is easier to deal with.
- In HDR, as advised in 'Main image', contrast slider must be visually tuned because source material is not always 'fitting well' in terms of actual data and HDR metadata used by the tone-mapping.
  - The projector seems to reach peak luminance on a 500 nits source for a 50 contrast (with brightness near 50, to be accurate): In other words it means that if a pixel in the signal really reaches 500 nits and the contrast is set to 50, its actual rendered brightness will indeed fit just well within max physical capabilities of the projector. So if your input signal is tone-mapped for 150nits max, you won't ever reach the physical peak brightness since CONTRAST slider stops at 100 and 166 would be the good value.
    - It also means that, very probably, the HDR10 tone-mapping applied is fixed and set at 500nits maxlum. If I'm not mistaken, it would be a shame because the real peak maxlum nits of this projector with various screens is somwhere between 100 and 300, absolutely not 500 (If you find an affordable projector on the market with such brightness power, please ping me).
    - Formula to have your contrast setting based on LLDV-maxlum : ``contrast_value = (1/(LLDV-maxlum/500))*50`` (EDIT: this is an approximation as contrast 0 is not really contrast 0, possibly the absolute 0 is at -10 and thus unreachable with UI, and peak brithness is maybe at contrast 40 with 500 nits).
    - It also explains why some people had better results applying (maybe by mistake) a second tone-mapping due to HDR10 metadata override set on the HDFURY device. If HDR MaxCLL = LLDV maxlum, it basically says the Formovie to tone-map the input signal from lldv-maxlum-value to 500nits, resolving the peak brightness issue but applying 2 tone-mappings in a row.
    - neutral HDR setting in HDfury is ``87:01:1a:5c:02:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00`` 
- In native Dolby Vision mode, Formovie has opted to cap the max "digital" brigthness to roughly half of the projector/s capabilities. It's maybe to ensure consistant color calibration across luminosity.
  - Increasing contrast does not fix the issue, it crushes bright lights even more even though it increases peak brightness. LLDV trick is the solution to break that limit.
  - In recent firmware update, there is a new "DV vivid" mode. I think it's better but not yet on par with LLDV trick.

> [!CAUTION]
> Online reviews are measuring contrast without taking all the above into account and they come up with contrast values that are lower in HDR mode than in SDR.

## Color temperature
--  | value
---- | ----
R | -2
G | -8
B | -28

> might be a little "cooler" than projector central's advised one (d65) but it's a compromise to keep some more gamut coverage.

## Color management

> - Gamma has to be set to middle for these settings to work
> - Maybe worth trying with gamma bright and all brightness cursors to 50

-- | HUE | SATURATION | BRIGHTNESS
---- | ---- | ---- | ----
R | 52 | 52* | 61*
G | 41 | 54* | 60*
B | 51 | 50 | 69*
C | 57 | 46 | 68*
M | 40 | 55* | 63* 
Y | 55* | 50* | 59* 
FT | 48 | 48* | 52*

--  | OFFSET |  GAIN
---- | ---- | ----
R | 48* | 48*
G | 50 | 48*
B | 50 | 48*

> - HUE settings are the same as https//www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm excecpt for yellow.
> - SATURATION lowered for RED, FT and MAGENTA.
> - BRIGHTNESS lowered by a lot. Worth trying 50 with Gamma bright as well maybe.
> - GAIN adusted to same value for all, should be adjusted with COLOR TEMPERATURE instead.
>   - (Maybe this improves contrast at the expense of color gammut and the other way around improves color gammut at the expense of contrast, or maybe both are digital and completely similar) 
> - RED must be lowered by 2 units from default in both GAIN and COLOR TEMPERATURE sections (giving 48 and -2) to avoid pink/purple noise on bright lights
> - ``*`` means it was changed from projectorcentral advice


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
>   - ``De-counter`` set to ``low`` or ``middle`` to mitigate color banding artefacts. 
>   - ``MPEG NR`` set to  ``low`` or ``middle`` to mitigate compression artefacts.
> - ``DNR`` gives smearing effects sometimes. I think it must be avoided.  

> [!TIP]
> - Tone-mapping to SDR will only fix this issue marginally, but is also a good solution if your player device has good HDR to SDR tone-mapping, especially if your screen max luminosity is around 100 nits (as 100 nits value is often used for the HDR to SDR tone-mapping).
> - ``Advanced video`` > ``Adaptive luma control`` set to ``middle`` (other values are suboptimal IMHO) can be great in SDR and can help in pure HDR too, but it's also matter of taste and it's somewhat breaking the director's intent.

## 11 points white balance correction
I found correction to be very subtle but great anyway : https://www.projectorcentral.com/Formovie-Theater-UST-Laser-TV-Projector-Review.htm . And this theorically helps to change global white balance while keeping hus/saturation the same.

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
