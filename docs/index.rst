+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
splinter - python acceptance testing for web applications 
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

`what's new in splinter 0.0.2? <http://splinter.cobrateam.info/news.html>`_

install
=======

::

	$ [sudo] pip install splinter

development
===========

* Source hosted at `GitHub <http://github.com/cobrateam/splinter>`_
* Report issues on `GitHub Issues <http://github.com/cobrateam/splinter/issues>`_

Pull requests are very welcome! Make sure your patches are well tested.

running the tests
-----------------

if you are using a virtualenv, all you need is:

::

    $ make test

community
---------

#cobrateam channel on irc.freenode.net

documentation
=============

Browser
-------

To use splinter you need create a Browser instance:

::

    from splinter.browser import Browser
    browser = Browser()


splinter support three drivers: chrome, firefox and zopetestbrowser

::

	browser = Browser('webdriver.chrome')
	browser = Browser('webdriver.firefox')
	browser = Browser('zope.testbrowser')
	
Navigating with Browser.visit
-----------------------------

You can use the ``visit`` method to navigate to other pages:

::
    
    browser.visit('http://cobrateam.info')

The ``visit`` method takes only a single parameter - the ``url`` to be visited.

Browser.title
-------------

You can get the title of the visited page using the ``title`` attribute:

::

    browser.title
    
Verifying page content with Browser.html
----------------------------------------

You can use the ``html`` attribute to get the html content of the visited page:

::

    browser.html
    
Verifying page url with Browser.url
-----------------------------------

The visited page's url can be accessed by the ``url`` attribute:
    
::

    browser.url
    
Finding elements
----------------

For finding elements you can use five methods, one for each selector type ``css_selector``, ``xpath``, ``tag``, ``name``, ``id``::

    browser.find_by_css_selector('h1')
    browser.find_by_xpath('//h1')
    browser.find_by_tag('h1')
    browser.find_by_name('name')
    browser.find_by_id('firstheader')

These methods returns a list of all found elements.

	
you can get the first found element:

::

	browser.find_by_name('name').first

You can use too the last attribute, that returns the last found element:

::

	browser.find_by_name('name').last

Get element using index
-----------------------

You also use index for get a element

::

	browser.find_by_name('name')[1]
	
all elements and find_by_id
----------------------------

A web page should be only one id per page. Then find_by_id() method return always a list with one element.
    
Finding links
-------------

For finding link elements you can use ``find_link_by_text`` or ``find_link_by_href``:

::

    browser.find_link_by_text('Link for Example.com')
    
or

::

    browser.find_link_by_href('http://example.com')

These methods returns a list of all found elements.

For finding links by id, tag, name or xpath you should use other find methods (``find_by_css_selector``, ``find_by_xpath``, ``find_by_tag``, ``find_by_name`` and ``find_by_id``).


Get element value
-----------------

In order to retrieve an element's value, use the ``value`` property:

::

    browser.find_by_css_selector('h1').first.value

or

::

    element = browser.find_by_css_selector('h1').first
    element.value


Clicking links and buttons
--------------------------

You can click in links and buttons. splinter follows any redirects, and submits forms associated with buttons.

::

	browser.find_by_name('send').first.click()
	
or

::

	browser.find_link_by_text('my link').first.click()
	
    
Interacting with forms
----------------------

::

    browser.fill_in('query', 'my name')
    browser.attach_file('file', '/path/to/file/somefile.jpg')    
    browser.choose('some-radio')
    browser.check('some-check')
    browser.uncheck('some-check')
    browser.select('uf', 'rj')
    
Verifying if element is visible or invisible
--------------------------------------------

To check if an element is visible or invisible, use the ``visible`` property. For instance:

::

    browser.find_by_css_selector('h1').first.visible

will be True if the element is visible, or False if it is invisible.

Executing javascript
--------------------

You can easily execute JavaScript, in drivers which support it:

::

    browser.execute_script("$('body').empty()")
    
You can return the result of the script:

::

    browser.evaluate_script("4+4") == 8
