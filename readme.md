# Genja

## Introduction

Genja is a minimalist static website generator built on top of Jinja2. 
It allows you to easily create static website with the ease of the powerful templating library, [Jinja2](https://jinja.pocoo.org/docs/latest/). 

## How to use it?

Download ``genja.py``. It is a simple command-line interface that must be used to generate your website. Simply type ``python genja.py`` to create pages in the ``output`` directory. 

Genja relies on some libraries to work. Type ``pip install -r requirements.txt`` to install them. 

## How to structure my website?

The ``static`` folder will be copied as-is in the ``output`` folder. Use it to store your assets, css, js, etc. 

Both ``content`` and ``templates`` folders contain the templates that are required by Jinja2. By convention, use the ``templates`` folder to put those who corresponds to your layout and are not specific to a page. The ones in ``content`` will be used to generate the pages of your website. 

Each file in ``content`` that does not start with an underscore and that ends with ``.html`` will be processed and converted in exactly one page in the ``output`` directory. 

The default folders can be changed in ``genja.py``. 
By default, all the files that are contained in the ``output`` folder will be removed when using the script. Be careful!

## What else?

While processing the templates, the context of Jinja2 will be provided with some filters and values: 

 - A filter ``|relative`` which translates a path relative to the root of the website to a path relative to current page location. For instance, if you use ``"A/page.html"|relative`` in ``B/test.html`` (under ``pages``), it will be translated to ``../A/page.html``. This allows you to define links without having to worry about what will be the root URL. 
  - A filter ``|parse_date`` that takes a string representing a date and tries to convert it into a Python ``datetime`` object. This uses ``dateutil.parser.parse``. 
  - A filter ``|format_date`` that format a Python ``datetime`` object using given format (a default one is provided). 
  - A dyanmic value ``page`` that equals the relative path (starting from the ``content`` folder) of the page being processed. 
