Introduction
============

.. image:: https://readthedocs.org/projects/adafruit-circuitpython-st7735/badge/?version=latest
    :target: https://circuitpython.readthedocs.io/projects/st7735/en/latest/
    :alt: Documentation Status

.. image:: https://img.shields.io/discord/327254708534116352.svg
    :target: https://discord.gg/nBQh6qu
    :alt: Discord

.. image:: https://travis-ci.com/adafruit/Adafruit_CircuitPython_ST7735.svg?branch=master
    :target: https://travis-ci.com/adafruit/Adafruit_CircuitPython_ST7735
    :alt: Build Status

displayio driver for ST7735 TFT-LCD displays.

Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython 4.0.0-beta.0+ <https://github.com/adafruit/circuitpython>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://github.com/adafruit/Adafruit_CircuitPython_Bundle>`_.

Usage Example
=============

.. code-block:: python
    import adafruit_st7735
    import board
    import busio
    import displayio
    import time

    displayio.release_displays()

    spi = busio.SPI(board.SCL, board.SDA)
    bus = displayio.FourWire(spi, chip_select=board.D9, command=board.D7, reset=board.D8)
    display = adafruit_st7735.ST7735(bus, width=128, height=128)

    s = displayio.Shape(10, 10)
    p = displayio.Palette(2)
    p[1] = 0xff0000
    s = displayio.Sprite(s, pixel_shader=p, position=(0,0))
    everything = displayio.Group(max_size=10)
    everything.append(s)
    display.show(everything)

    time.sleep(10)

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/adafruit/Adafruit_CircuitPython_ST7735/blob/master/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.

Building locally
================

Zip release files
-----------------

To build this library locally you'll need to install the
`circuitpython-build-tools <https://github.com/adafruit/circuitpython-build-tools>`_ package.

.. code-block:: shell

    python3 -m venv .env
    source .env/bin/activate
    pip install circuitpython-build-tools

Once installed, make sure you are in the virtual environment:

.. code-block:: shell

    source .env/bin/activate

Then run the build:

.. code-block:: shell

    circuitpython-build-bundles --filename_prefix adafruit-circuitpython-st7735 --library_location .

Sphinx documentation
-----------------------

Sphinx is used to build the documentation based on rST files and comments in the code. First,
install dependencies (feel free to reuse the virtual environment from above):

.. code-block:: shell

    python3 -m venv .env
    source .env/bin/activate
    pip install Sphinx sphinx-rtd-theme

Now, once you have the virtual environment activated:

.. code-block:: shell

    cd docs
    sphinx-build -E -W -b html . _build/html

This will output the documentation to ``docs/_build/html``. Open the index.html in your browser to
view them. It will also (due to -W) error out on any warning like Travis will. This is a good way to
locally verify it will pass.