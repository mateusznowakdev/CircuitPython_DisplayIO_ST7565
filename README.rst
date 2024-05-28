Introduction
============

.. image:: https://github.com/mateusznowakdev/CircuitPython_DisplayIO_ST7565/workflows/Build%20CI/badge.svg
    :target: https://github.com/mateusznowakdev/CircuitPython_DisplayIO_ST7565/actions
    :alt: Build Status

.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/psf/black
    :alt: Code Style: Black

CircuitPython displayio library for ST7565 and ST7567 controllers, based on the original framebuf implementation.

As a community effort, this library was tested with only one ST7567 display and may be not fully compatible with other hardware.

Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython <https://github.com/adafruit/circuitpython>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://circuitpython.org/libraries>`_
or individual libraries can be installed using
`circup <https://github.com/adafruit/circup>`_.

Installing from PyPI
=====================
.. note:: This library is not available on PyPI yet. Install documentation is included
   as a standard element. Stay tuned for PyPI availability!

On supported GNU/Linux systems like the Raspberry Pi, you can install the driver locally `from
PyPI <https://pypi.org/project/circuitpython-displayio-st7565/>`_.
To install for current user:

.. code-block:: shell

    pip3 install circuitpython-displayio-st7565

To install system-wide (this may be required in some cases):

.. code-block:: shell

    sudo pip3 install circuitpython-displayio-st7565

To install in a virtual environment in your current project:

.. code-block:: shell

    mkdir project-name && cd project-name
    python3 -m venv .venv
    source .env/bin/activate
    pip3 install circuitpython-displayio-st7565

Installing to a Connected CircuitPython Device with Circup
==========================================================

Make sure that you have ``circup`` installed in your Python environment.
Install it with the following command if necessary:

.. code-block:: shell

    pip3 install circup

With ``circup`` installed and your CircuitPython device connected use the
following command to install:

.. code-block:: shell

    circup install displayio_st7565

Or the following command to update an existing version:

.. code-block:: shell

    circup update

Usage Example
=============

.. code-block:: python

    import board
    import busio
    import displayio
    import terminalio

    from adafruit_display_text import label
    import displayio_st7565

    # Compatibility with both CircuitPython 8.x.x and 9.x.x.
    # Remove after 8.x.x is no longer a supported release.
    try:
        from fourwire import FourWire
    except ImportError:
        from displayio import FourWire

    displayio.release_displays()

    spi = busio.SPI(board.GP18, board.GP19)
    display_bus = FourWire(
        spi, command=board.GP20, chip_select=board.GP17, reset=board.GP21, baudrate=1000000
    )

    display = displayio_st7565.ST7565(display_bus, width=128, height=64)

    splash = displayio.Group()
    display.root_group = splash

    text = "Hello World!"
    text_area = label.Label(terminalio.FONT, text=text, color=0xFFFFFF, x=0, y=8)
    splash.append(text_area)

    while True:
        pass

Documentation
=============
API documentation for this library can be found on `Read the Docs <https://circuitpython-displayio-st7565.readthedocs.io/>`_.

For information on building library documentation, please check out
`this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/mateusznowakdev/CircuitPython_DisplayIO_ST7565/blob/HEAD/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.
