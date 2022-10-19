Getting Started
===================================

The main concept bethind BunyipFormBuilder is to have the PHP code mirror as closely as possible the structure of the HTML form elements.
Each HTML form element has the following corresponding PHP classes:
  *  Element class
  *  Template class (one or more)
  
For example if we look at one of the most common HTML form elements the 'input' element (technically it is the text element), it looks something like

.. code-block:: html

  <input type="text" id="fname" name="fname">
  
In the example above we see three attributes on the <input /> tag, 'type', 'id' and 'name'
  
When instantiating the TextFormBuilder class we can pass into the class constructor the attributes that the form element supports.
  
.. code-block:: php

    $text = new TextFormBuilder(['id'=>'fname', 'name'=>'fname']);
    
When rendered this new TextFormBuilder object will create something like the HTML shown above.

If I pass in an attribute which isn't supported by the form element, like an attribute of 'foo' with a value of 'bar' it does not get added to the form element.  Which means that form element attributes are 'white-listed'.  Only defined attributes can be used.
