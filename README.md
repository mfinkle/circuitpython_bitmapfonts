## Introduction
Adafruit's framebuf library supports some bitmap font rendering capabilities. The library already includes a bitmap font render (`BitmapFont`) and a classic 5x8 based font, called `font5x8.bin`. CircuitPython BitmapFonts ships a 3x8 based font which can be useful for smaller displays.

## Dependencies
This code depends on:

* [Adafruit CircuitPython](https://github.com/adafruit/circuitpython)
* [Adafruit framebuf](https://github.com/adafruit/Adafruit_CircuitPython_framebuf)

Please make sure all dependencies are available on the CircuitPython filesystem.

## Usage Example
```
import board
import neopixel

from adafruit_led_animation.color import AMBER
from adafruit_led_animation.grid import PixelGrid, VERTICAL

from textscroll_animation import TextScroll

# Update to match the pin connected to your NeoPixels
pixel_pin = board.D6
# Update to match the number of NeoPixels you have connected
pixel_num = 64

pixels = neopixel.NeoPixel(pixel_pin, pixel_num, brightness=0.1, auto_write=False)

# Set the size of the sprite to 8 pixels wide by 8 pixels tall
# (make sure 'orientation', 'alternating' and 'reverse_x' are correct for your display)
grid = PixelGrid(pixels, 8, 8, orientation=VERTICAL, alternating=False, reverse_x=True)

# TextScroll defaults to using 'font5x8.bin' so we need to explicitly use a different font.
# Make sure the font file is on the device
text_scroll = TextScroll(grid, 0.1, 'Hello World', color=AMBER, font_name='font3x8.bin')

while True:
    text_scroll.animate()
```

## What's Included
**font3x8_to_bin.py**

* Script that contains the raw bitmap font structure for font3x8. You can generate the binary file by running `python3 font3x8_to_bin.py`.

**font3x8.bin**

* Binary font3x8 file, ready to be used with [Adafruit framebuf](https://github.com/adafruit/Adafruit_CircuitPython_framebuf) `FrameBuffer` and `BitmapFont` based code.
