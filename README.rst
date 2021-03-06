django-cities-tiny -- *Simple django-cities alternative*
=========================================================

This add-on provides models and commands to import country/zone/city data into your
database.
The data is pulled from `GeoNames
<http://www.geonames.org/>`_ and contains:

  - country names
  - administrative division zones
  - city names

Spatial query support is not required by this application.

This application is very simple and is useful if you want to make a simple
address book for example. If you intend to build a fully featured spatial
database, you should use
`django-cities
<https://github.com/coderholic/django-cities>`_.

This is a fork of django-cities-light by James Pic. The main difference of
django-cities-tiny is:

  - support for localized names (from alternateNames.txt)
  - support for administrative division zones (from admin1CodesASCII.txt,
    admin2Codes.txt, or from XX.txt)
  - required Django 1.0+, Python 2.3+ and no other dependences

Installation
------------

Install django-cities-tiny::

    easy_install django-cities-tiny

Add `cities_tiny` to your `INSTALLED_APPS`.

Now, run syncdb, it will create all required tables for models::

    ./manage.py syncdb

Data update
-----------

Finnaly, populate your database with command::

    ./manage.py citiestinyrefresh

This command is well documented, consult the help with::
    
    ./manage.py help citiestinyrefresh

Limiting data to import
---------------------

If you want to import only cities from France, USA and Belgium you could do as
such in your settings.py::

    CITIES_TINY_COUNTRIES = ('FR', 'US', 'BE')

Configure logging
-----------------

To get output from citiestinyrefresh command simply pass the -v2 or or
--verbosity=2 option. Also if you use Django 1.3+, you may configure logging
system in your settings.py, simply configure a handler and formatter for
`cities_tiny` logger. For example::

    LOGGING = {
        'version': 1,
        'disable_existing_loggers': False,
        'formatters': {
            'simple': {
                'format': '%(levelname)s %(message)s'
            },
        },
        'handlers': {
            'console':{
                'level':'DEBUG',
                'class':'logging.StreamHandler',
                'formatter': 'simple'
            },
        },
        'loggers': {
            'cities_tiny': {
                'handlers':['console'],
                'propagate': True,
                'level':'DEBUG',
            },
            # also use this one to see SQL queries
            'django': {
                'handlers':['console'],
                'propagate': True,
                'level':'DEBUG',
            },
        }
    }
