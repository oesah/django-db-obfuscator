====================
Django DB Obfuscator
====================


.. image:: https://img.shields.io/pypi/v/django-db-obfuscator.svg
        :target: https://pypi.python.org/pypi/django-db-obfuscator

.. image:: https://img.shields.io/travis/oesah/django-db-obfuscator.svg
        :target: https://travis-ci.com/oesah/django-db-obfuscator

.. image:: https://readthedocs.org/projects/django-db-obfuscator/badge/?version=latest
        :target: https://django-db-obfuscator.readthedocs.io/en/latest/?badge=latest
        :alt: Documentation Status

.. image:: https://pyup.io/repos/github/oesah/django-db-obfuscator/shield.svg
     :target: https://pyup.io/repos/github/oesah/django-db-obfuscator/
     :alt: Updates


Django app to obfuscate text data. Originally develop by `Dipcode Software <https://github.com/dipcode-software>`_.

Compatibility
-------------
Tested with python 3.6, 3.7, 3.8 and Django 1.11 & 2.2: `Travis CI <https://travis-ci.org/dipcode-software/django-obfuscate>`_

How to install
--------------

To install the app run:

.. code:: shell

    $ pip install django-db-obfuscater

or add it to the list of requirements of your project.

Then add ‘obfuscator’ to your INSTALLED\_APPS.

.. code:: python

    INSTALLED_APPS = [
        ...
        'obfuscator',
    ]

Example usage
-------------

On you django project settings, configure the model names and field
names to be obfuscated:

.. code:: python

    OBFUSCATOR = {
        'FIELDS': {
            'app_label.ModelClass1': ['field1', 'field2', 'field3'],
            'app_label.ModelClass2': ['field1'],
            // ...
        }
    }

Run the management command to start obfuscation:

.. code:: shell

    $ python manage.py obfuscate

You can run the management command passing as arguments: a model class
path and a list of fields to obfuscate (thus will ignore ``FIELDS``
setting):

.. code:: shell

    $ python manage.py obfuscate --model=app_label.ModelClass1 --fields=field1, field2, field3

Settings reference
------------------

OBFUSCATOR\_CLASS
~~~~~~~~~~~~~~~~~

Default: ``obfuscator.utils.ObfuscatorUtils``

Path to class where obfuscator methods are defined. By default, the
class define tow obfuscator methods: \* ``text`` - Obfuscate simple text
data, respecting ``max-length`` field parameter; \* ``email`` -
Obfuscate email data. Only text before ``@`` is obfuscated, respecting
``max-length`` field parameter.

This class also define an ``obfuscate`` method. This method use fields
mapping (see ``FIELDS_MAPPING`` setting) to route the field type with
the obfuscate method.

You can redefine this class by subclassing the default class and
changing this setting to point to your class.

FIELDS\_MAPPING
~~~~~~~~~~~~~~~

Default:

.. code:: python

    {
        models.CharField: 'text',
        models.TextField: 'text',
        models.EmailField: 'email'
    }

Map django model field types with obfuscator methods.

FIELDS
~~~~~~

Default: ``{}``

Fields to be obfuscated and respective model class path. Must be a
``dict`` with keys as python dot notation to path where the models are
declared and the values must be declared as lists of model fields.

If no value defined, the management command will do nothing.

Example:

.. code:: python

    {
        'contenttypes.ContentType': ['model', 'label'],
        // ...
    }

License
-------

MIT license, see the LICENSE file. You can use obfuscator in open source
projects and commercial products.


Sponsorship
-----------

This project is maintained by `Mathison AG | Mobile & Web Development <https://mathison.ch>`_.
