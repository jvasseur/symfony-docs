.. index::
    single: Symfony Twig extensions

.. _symfony2-twig-extensions:

Symfony Twig Extensions
=======================

Twig is the default template engine for Symfony. By itself, it already contains
a lot of built-in functions, filters, tags and tests (learn more about them
from the `Twig Reference`_).

Symfony adds custom extensions on top of Twig to integrate some components
into the Twig templates. The following sections describe the custom
:ref:`functions <reference-twig-functions>`, :ref:`filters <reference-twig-filters>`,
:ref:`tags <reference-twig-tags>` and :ref:`tests <reference-twig-tests>`
that are available when using the Symfony Core Framework.

There may also be tags in bundles you use that aren't listed here.

.. _reference-twig-functions:

Functions
---------

.. _reference-twig-function-render:

render
~~~~~~

.. code-block:: twig

    {{ render(uri, options = []) }}

``uri``
    **type**: ``string`` | ``ControllerReference``
``options`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Renders the fragment for the given controller (using the `controller`_ function)
or URI. For more information, see :ref:`templating-embedding-controller`.

The render strategy can be specified in the ``strategy`` key of the options.

.. tip::

    The URI can be generated by other functions, like `path`_ and `url`_.

.. _reference-twig-function-render-esi:

render_esi
~~~~~~~~~~

.. code-block:: twig

    {{ render_esi(uri, options = []) }}

``uri``
    **type**: ``string`` | ``ControllerReference``
``options`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Generates an ESI tag when possible or falls back to the behavior of
`render`_ function instead. For more information, see
:ref:`templating-embedding-controller`.

.. tip::

    The URI can be generated by other functions, like `path`_ and `url`_.

.. tip::

    The ``render_esi()`` function is an example of the shortcut functions
    of ``render``. It automatically sets the strategy based on what's given
    in the function name, e.g. ``render_hinclude()`` will use the hinclude.js
    strategy. This works for all ``render_*()`` functions.

controller
~~~~~~~~~~

.. code-block:: twig

    {{ controller(controller, attributes = [], query = []) }}

``controller``
    **type**: ``string``
``attributes`` *(optional)*
    **type**: ``array`` **default**: ``[]``
``query`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Returns an instance of ``ControllerReference`` to be used with functions
like :ref:`render() <reference-twig-function-render>` and
:ref:`render_esi() <reference-twig-function-render-esi>`.

asset
~~~~~

.. code-block:: twig

    {{ asset(path, packageName = null, absolute = false, version = null) }}

``path``
    **type**: ``string``
``packageName`` *(optional)*
    **type**: ``string`` | ``null`` **default**: ``null``
``absolute`` (deprecated as of 2.7)
    **type**: ``boolean`` **default**: ``false``
``version`` (deprecated as of 2.7)
    **type**: ``string`` **default** ``null``

Returns a public path to ``path``, which takes into account the base path
set for the package and the URL path. More information in
:ref:`book-templating-assets`. For asset versioning, see
:ref:`reference-framework-assets-version`.

assets_version
~~~~~~~~~~~~~~

.. code-block:: twig

    {{ assets_version(packageName = null) }}

``packageName`` *(optional)*
    **type**: ``string`` | ``null`` **default**: ``null``

Returns the current version of the package, more information in
:ref:`book-templating-assets`.

form
~~~~

.. code-block:: twig

    {{ form(view, variables = []) }}

``view``
    **type**: ``FormView``
``variables`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Renders the HTML of a complete form, more information in
:ref:`the Twig Form reference <reference-forms-twig-form>`.

form_start
~~~~~~~~~~

.. code-block:: twig

    {{ form_start(view, variables = []) }}

``view``
    **type**: ``FormView``
``variables`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Renders the HTML start tag of a form, more information in
:ref:`the Twig Form reference <reference-forms-twig-start>`.

form_end
~~~~~~~~

.. code-block:: twig

    {{ form_end(view, variables = []) }}

``view``
    **type**: ``FormView``
``variables`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Renders the HTML end tag of a form together with all fields that have not
been rendered yet, more information in
:ref:`the Twig Form reference <reference-forms-twig-end>`.

form_enctype
~~~~~~~~~~~~

.. code-block:: twig

    {{ form_enctype(view) }}

``view``
    **type**: ``FormView``

Renders the required ``enctype="multipart/form-data"`` attribute if the
form contains at least one file upload field, more information in
:ref:`the Twig Form reference <reference-forms-twig-enctype>`.

form_widget
~~~~~~~~~~~

.. code-block:: twig

    {{ form_widget(view, variables = []) }}

``view``
    **type**: ``FormView``
``variables`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Renders a complete form or a specific HTML widget of a field, more information
in :ref:`the Twig Form reference <reference-forms-twig-widget>`.

form_errors
~~~~~~~~~~~

.. code-block:: twig

    {{ form_errors(view) }}

``view``
    **type**: ``FormView``

Renders any errors for the given field or the global errors, more information
in :ref:`the Twig Form reference <reference-forms-twig-errors>`.

form_label
~~~~~~~~~~

.. code-block:: twig

    {{ form_label(view, label = null, variables = []) }}

``view``
    **type**: ``FormView``
``label`` *(optional)*
    **type**: ``string`` **default**: ``null``
``variables`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Renders the label for the given field, more information in
:ref:`the Twig Form reference <reference-forms-twig-label>`.

form_row
~~~~~~~~

.. code-block:: twig

    {{ form_row(view, variables = []) }}

``view``
    **type**: ``FormView``
``variables`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Renders the row (the field's label, errors and widget) of the given field,
more information in :ref:`the Twig Form reference <reference-forms-twig-row>`.

form_rest
~~~~~~~~~

.. code-block:: twig

    {{ form_rest(view, variables = []) }}

``view``
    **type**: ``FormView``
``variables`` *(optional)*
    **type**: ``array`` **default**: ``[]``

Renders all fields that have not yet been rendered, more information in
:ref:`the Twig Form reference <reference-forms-twig-rest>`.

csrf_token
~~~~~~~~~~

.. code-block:: twig

    {{ csrf_token(intention) }}

``intention``
    **type**: ``string``

Renders a CSRF token. Use this function if you want CSRF protection without
creating a form.

is_granted
~~~~~~~~~~

.. code-block:: twig

    {{ is_granted(role, object = null, field = null) }}

``role``
    **type**: ``string``
``object`` *(optional)*
    **type**: ``object``
``field`` *(optional)*
    **type**: ``string``

Returns ``true`` if the current user has the required role. Optionally,
an object can be pasted to be used by the voter. More information can be
found in :ref:`book-security-template`.

.. note::

    You can also pass in the field to use ACE for a specific field. Read
    more about this in :ref:`cookbook-security-acl-field_scope`.

logout_path
~~~~~~~~~~~

.. code-block:: twig

    {{ logout_path(key = null) }}

``key`` *(optional)*
    **type**: ``string``

Generates a relative logout URL for the given firewall. If no key is provided,
the URL is generated for the current firewall the user is logged into.

logout_url
~~~~~~~~~~

.. code-block:: twig

    {{ logout_url(key = null) }}

``key`` *(optional)*
    **type**: ``string``

Equal to the `logout_path`_ function, but it'll generate an absolute URL
instead of a relative one.

path
~~~~

.. code-block:: twig

    {{ path(name, parameters = [], relative = false) }}

``name``
    **type**: ``string``
``parameters`` *(optional)*
    **type**: ``array`` **default**: ``[]``
``relative`` *(optional)*
    **type**: ``boolean`` **default**: ``false``

Returns the relative URL (without the scheme and host) for the given route.
If ``relative`` is enabled, it'll create a path relative to the current
path. More information in :ref:`book-templating-pages`.

url
~~~

.. code-block:: twig

    {{ url(name, parameters = [], schemeRelative = false) }}

``name``
    **type**: ``string``
``parameters`` *(optional)*
    **type**: ``array`` **default**: ``[]``
``schemeRelative`` *(optional)*
    **type**: ``boolean`` **default**: ``false``

Returns the absolute URL (with scheme and host) for the given route. If
``schemeRelative`` is enabled, it'll create a scheme-relative URL. More
information in :ref:`book-templating-pages`.

absolute_url
~~~~~~~~~~~~

.. versionadded:: 2.7
    The ``absolute_url()`` function was introduced in Symfony 2.7.

.. code-block:: jinja

    {{ absolute_url(path) }}

``path``
    **type**: ``string``

Returns the absolute URL from the passed relative path. For example, assume
you're on the following page in your app:
``http://example.com/products/hover-board``.

.. code-block:: jinja

    {{ absolute_url('/human.txt') }}
    {# http://example.com/human.txt #}

    {{ absolute_url('products_icon.png') }}
    {# http://example.com/products/products_icon.png #}

relative_path
~~~~~~~~~~~~~

.. versionadded:: 2.7
    The ``relative_path()`` function was introduced in Symfony 2.7.

.. code-block:: jinja

    {{ relative_path(path) }}

``path``
    **type**: ``string``

Returns the relative path from the passed absolute URL. For example, assume
you're on the following page in your app:
``http://example.com/products/hover-board``.

.. code-block:: jinja

    {{ relative_path('http://example.com/human.txt') }}
    {# ../human.txt #}

    {{ relative_path('http://example.com/products/products_icon.png') }}
    {# products_icon.png #}

expression
~~~~~~~~~~

Creates an :class:`Symfony\\Component\\ExpressionLanguage\\Expression` in
Twig. See ":ref:`Template Expressions <book-security-template-expression>`".

.. _reference-twig-filters:

Filters
-------

.. _reference-twig-humanize-filter:

humanize
~~~~~~~~

.. code-block:: twig

    {{ text|humanize }}

``text``
    **type**: ``string``

Makes a technical name human readable (i.e. replaces underscores by spaces
or transforms camelCase text like ``helloWorld`` to ``hello world``
and then capitalizes the string).

.. versionadded:: 2.3
    Transforming camelCase text into human readable text was introduced in
    Symfony 2.3.

trans
~~~~~

.. code-block:: twig

    {{ message|trans(arguments = [], domain = null, locale = null) }}

``message``
    **type**: ``string``
``arguments`` *(optional)*
    **type**: ``array`` **default**: ``[]``
``domain`` *(optional)*
    **type**: ``string`` **default**: ``null``
``locale`` *(optional)*
    **type**: ``string`` **default**: ``null``

Translates the text into the current language. More information in
:ref:`Translation Filters <book-translation-filters>`.

transchoice
~~~~~~~~~~~

.. code-block:: twig

    {{ message|transchoice(count, arguments = [], domain = null, locale = null) }}

``message``
    **type**: ``string``
``count``
    **type**: ``integer``
``arguments`` *(optional)*
    **type**: ``array`` **default**: ``[]``
``domain`` *(optional)*
    **type**: ``string`` **default**: ``null``
``locale`` *(optional)*
    **type**: ``string`` **default**: ``null``

Translates the text with pluralization support. More information in
:ref:`Translation Filters <book-translation-filters>`.

yaml_encode
~~~~~~~~~~~

.. code-block:: twig

    {{ input|yaml_encode(inline = 0, dumpObjects = false) }}

``input``
    **type**: ``mixed``
``inline`` *(optional)*
    **type**: ``integer`` **default**: ``0``
``dumpObjects`` *(optional)*
    **type**: ``boolean`` **default**: ``false``

Transforms the input into YAML syntax. See :ref:`components-yaml-dump` for
more information.

yaml_dump
~~~~~~~~~

.. code-block:: twig

    {{ value|yaml_dump(inline = 0, dumpObjects = false) }}

``value``
    **type**: ``mixed``
``inline`` *(optional)*
    **type**: ``integer`` **default**: ``0``
``dumpObjects`` *(optional)*
    **type**: ``boolean`` **default**: ``false``

Does the same as `yaml_encode() <yaml_encode>`_, but includes the type in
the output.

abbr_class
~~~~~~~~~~

.. code-block:: twig

    {{ class|abbr_class }}

``class``
    **type**: ``string``

Generates an ``<abbr>`` element with the short name of a PHP class (the
FQCN will be shown in a tooltip when a user hovers over the element).

abbr_method
~~~~~~~~~~~

.. code-block:: twig

    {{ method|abbr_method }}

``method``
    **type**: ``string``

Generates an ``<abbr>`` element using the ``FQCN::method()`` syntax. If
``method`` is ``Closure``, ``Closure`` will be used instead and if ``method``
doesn't have a class name, it's shown as a function (``method()``).

format_args
~~~~~~~~~~~

.. code-block:: twig

    {{ args|format_args }}

``args``
    **type**: ``array``

Generates a string with the arguments and their types (within ``<em>`` elements).

format_args_as_text
~~~~~~~~~~~~~~~~~~~

.. code-block:: twig

    {{ args|format_args_as_text }}

``args``
    **type**: ``array``

Equal to the `format_args`_ filter, but without using HTML tags.

file_excerpt
~~~~~~~~~~~~

.. code-block:: twig

    {{ file|file_excerpt(line = null) }}

``file``
    **type**: ``string``
``line`` *(optional)*
    **type**: ``integer``

Generates an excerpt of seven lines around the given ``line``.

format_file
~~~~~~~~~~~

.. code-block:: twig

    {{ file|format_file(line, text = null) }}

``file``
    **type**: ``string``
``line``
    **type**: ``integer``
``text`` *(optional)*
    **type**: ``string`` **default**: ``null``

Generates the file path inside an ``<a>`` element. If the path is inside
the kernel root directory, the kernel root directory path is replaced by
``kernel.root_dir`` (showing the full path in a tooltip on hover).

format_file_from_text
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: twig

    {{ text|format_file_from_text }}

``text``
    **type**: ``string``

Uses `format_file`_ to improve the output of default PHP errors.

file_link
~~~~~~~~~

.. code-block:: twig

    {{ file|file_link(line = null) }}

``line`` *(optional)*
    **type**: ``integer``

Generates a link to the provided file (and optionally line number) using
a preconfigured scheme.

.. _reference-twig-tags:

Tags
----

form_theme
~~~~~~~~~~

.. code-block:: twig

    {% form_theme form resources %}

``form``
    **type**: ``FormView``
``resources``
    **type**: ``array`` | ``string``

Sets the resources to override the form theme for the given form view instance.
You can use ``_self`` as resources to set it to the current resource. More
information in :doc:`/cookbook/form/form_customization`.

trans
~~~~~

.. code-block:: twig

    {% trans with vars from domain into locale %}{% endtrans %}

``vars`` *(optional)*
    **type**: ``array`` **default**: ``[]``
``domain`` *(optional)*
    **type**: ``string`` **default**: ``string``
``locale`` *(optional)*
    **type**: ``string`` **default**: ``string``

Renders the translation of the content. More information in :ref:`book-translation-tags`.

transchoice
~~~~~~~~~~~

.. code-block:: twig

    {% transchoice count with vars from domain into locale %}{% endtranschoice %}

``count``
    **type**: ``integer``
``vars`` *(optional)*
    **type**: ``array`` **default**: ``[]``
``domain`` *(optional)*
    **type**: ``string`` **default**: ``null``
``locale`` *(optional)*
    **type**: ``string`` **default**: ``null``

Renders the translation of the content with pluralization support, more
information in :ref:`book-translation-tags`.

trans_default_domain
~~~~~~~~~~~~~~~~~~~~

.. code-block:: twig

    {% trans_default_domain domain %}

``domain``
    **type**: ``string``

This will set the default domain in the current template.

stopwatch
~~~~~~~~~

.. code-block:: jinja

    {% stopwatch 'name' %}...{% endstopwatch %}

This will time the run time of the code inside it and put that on the timeline
of the WebProfilerBundle.

.. _reference-twig-tests:

Tests
-----

selectedchoice
~~~~~~~~~~~~~~

.. code-block:: twig

    {% if choice is selectedchoice(selectedValue) %}

``choice``
    **type**: ``ChoiceView``
``selectedValue``
    **type**: ``string``

Checks if ``selectedValue`` was checked for the provided choice field. Using
this test is the most effective way.

Global Variables
----------------

.. _reference-twig-global-app:

app
~~~

The ``app`` variable is available everywhere and gives access to many commonly
needed objects and values. It is an instance of
:class:`Symfony\\Bundle\\FrameworkBundle\\Templating\\GlobalVariables`.

The available attributes are:

* ``app.user``
* ``app.request``
* ``app.session``
* ``app.environment``
* ``app.debug``
* ``app.security`` (deprecated as of 2.6)

Symfony Standard Edition Extensions
-----------------------------------

The Symfony Standard Edition adds some bundles to the Symfony Core Framework.
Those bundles can have other Twig extensions:

* **Twig Extensions** includes some interesting extensions that do not belong
  to the Twig core. You can read more in `the official Twig Extensions
  documentation`_.

.. _`Twig Reference`: http://twig.sensiolabs.org/documentation#reference
.. _`the official Twig Extensions documentation`: http://twig.sensiolabs.org/doc/extensions/index.html
