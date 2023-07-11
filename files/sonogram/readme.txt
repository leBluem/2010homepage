SonoGram 3.5 - 31. May 2012 - http://blumetools.dd-dns.de/

Freeware Windows (NTs4/2K/XP/V/7) program to draw a sonagram
(aka spectrogram, voiceprint, 3D spectrum or waterfall/energy plot) 
of audio data grabbed from a soundcards input/record channel or 
from an audio file.

bugs
----
    - if something seems to bve drawn wrong: try resizing the window or switch 
      fullscreen 

docu
----

  general
    This program evolved after I saw DSP Spectrum Tool for Winamp 2.0. 
    I wanted to make a free and standalone program. So here it is.

    Uses BASS audio library (bass.dll v2.4) from www.un4seen.com

    All options will be saved in an ini-file in the same directory as the binary.

    The control panel is movable by click and drag. Click right in the drawing 
    area to hide/show control panel.

    Make sure to select an active input/record channel and the right volume.

    For most controls there is some info if you move the mouse cursor over it.

    You have to play around a bit to find your best settings, 
    every source/music has its own characteristic.

  input
    list of available input devices/record channels from windows mixer

  open file
    Formats: MP3, OGG, WAV, AIFF (every format bass.dll can handle) 
    "open file" changes to a "stop" button on play
    when playing a file then input/record selection is disabled
    A filename as commandline parameter opens and plays it in a loop on wave channel.
    
    The image generated from a file played by sonogram itself is somewhat clearer 
    than playing with another player and than grabbing from soundcard (sum of noise 
    from audio processing devices).

  volume
    works for the selected input/record channel (system wide) or for the playing file
    
  checkbox right to volume
    dim the input level until no more clipping occurs
    clipping is visible with vol meter on (small rectangle at the maximum of vol meter)
    this option will not be saved
    
  draw mode
    try everyone!
    frequency scala and volume meter in "vsplit" mode only
    in mono "vsplit" is the same as "r->l"

  sample-rate 
    not every soundcard supports every one listed here
    set and fixed after opening a file
    for example audio from an analog TV-Signal will be cut at 16kHZ, 
    so one can use 16kHz*2 = 32kHz as SampleRate
    if you change this, "freqmax" changes too
    
  update interval 
    in ms to get data from soundcard/file [10...500]ms
    for me this interval changes in steps of 5ms only (21ms is the same as 25ms). 
    dont know if bass or my hardware limits this, so I set the increment to 1
    
  FFTsize
    datasize to retrieve from soundcard
    (e.g. 2 * 512 samples * 2 stereo channels = 2048)
    higher is not always more detailed, because more samples are interpolated to one pixel
    use "auto" to zoom to 100%
    
  blur
    amount of pixels to blur between [0..6]
    usefull (not only) with logarithmic frequency scale

  mono 
    in mono "vsplit" is the same as "r->l"
  
  swap l/r
    ...    (channel)
  
  dblpxl 
    2 pixels per interval (interpolated)
  
  splitline 
    if stereo show dotted splitline between channels
    
  Hz-info 
    only in "vsplit" mode
    show Hz-value (and equivalent Note) at mouse position
    show frequency scala
  
  vol meter
    only in "vsplit" mode (too lazy for the other modes)
    show volume level and average signal strength as bars and peaks
    clipping indicators (small rectangle at the maximum of the bar)

  save
    save BMP snapshot in program dir (app-wide Alt+S)
  
  auto 
    resize window / change Frequency to match FFTSize for an accurate draw
  
  full
    toggle fullscreen, Alt+Return (app-wide) / DoubleClick

  hide
    toggle control panel Esc (app-wide) / Right Mouse
  
  rst
    reset to default values
  
  exit
    Alt+X (app-wide)

  freqmin/freqmax
    control frequency range to draw
    
  amplitude scale
    brightness 1..255
    there are three different contrast modes (1 normal, 3 highest)
    
  frequency scale
    continuously adjustable from linear to logarithmic scale
    1         - linear
    up to 2.0 - logarithmic
    presets 1 from 2 steps of 0.125

  color controls
    < >           - shift palette left/right
    invert/random - ...
  
  color presets
      w - black/white
      r - red
      e - energy/orange
      y - yellow
      g - green
      b - blue
      v - violett
      1 - sun
      2 - light midtones violet/green/yellow/red
      3 - rainbow
      4 - light jungle
      5 - light background (fine tune palette sample)

  click on palette to set color for text/splitline

  click on a single color to select one with the standard color dialog
    right click on color 1 to generate gradient from color 1 to 4 (changing col2 and col3)
    right click on color 7 to generate gradient from color 4 to 7 (changing col5 and col6)
    right click on color 4 to generate gradient from color 1 to 4 AND from color 4 to 7 
      (changing col2, col3, col5 and col6)
  
  2 sliders control the color distribution in the palette
  the buttons below provide some presets
  
  click the wide button on the bottom to show 4 more sliders for finetuning the palette
  
history
-------

  v3.5 (31. May 2012)
    - fixed drawing average values; picture is sharper now
    - added phase-mode 

  v3.4 (1. Mar 2012)
    - fixed mixer synchronization

  v3.3 (23. Nov 2011, nonpublic)
    - added circle/radar mode
    - added "missing frames info"
    - fixed pixel incurracy (now a bit sharper)
    - contrast logarithmic
    - minor init fixes

  v3.2 (22. Juni 2011)
    - non scrolling mode
    - when vsplit,mono,levelmeter are on (default and on reset), there is some other visual on the left
    - fixed logarithmic frequency scaling
    - fixed bug when changing from higher to lower FFTsize
    - other minor bugs

  v3.1 (26. April 2010)
    - compiled with a clean delphi version!
    - fixed fullscreen restore
    - fixed some minor drawing errors
    - added volume, vol-meter, autolevel, fps info, zoom info
    - changed/improved amplitude scale
    - removed auto hide control panel
  
  v3.0 (1. March 2010)
    - complete rewrite of audio input and drawing
    - added max/min frequency, more colors, blur
    - added logarithmic freqency scale
    - improved colorpalette
    - removed record stuff
    - uses bassDLL v2.4
    
  v2.0 (10. Januar 2007)
    - uses bass.DLL v2.3

  v1.0 (21. Januar 2005, nonpublic)
    - uses bass.DLL v2.2

other programs
--------------

foobar2000.org has a builtin spectrogram plotter
winamp: AVS-Editor -> add (+) -> Render -> Timescope
spectrumlab http://freenet-homepage.de/dl4yhf/spectra1.html

linux baudline http://www.baudline.com
timidity http://www.onicos.com/staff/iz/timidity/
Layer-based Audio Editor http://www.oli4.ch/laoe/
sonic visualizer http://www.sonicvisualiser.org/
arss http://arss.sourceforge.net/ 
  is now PhotoSounder (commercial) http://photosounder.com/

http://www.youtube.com/watch?v=JzDDWkLw1ig
http://www.sengpielaudio.com/Rechner-notennamen.htm
