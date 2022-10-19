Usage
=====


Building a Form with a Fieldset
----------------

To create a simple form with a fieldset we will have code something like the following:

.. code-block:: php

	require_once '../Autoloader.php';
	use BunyipFormBuilder\FormBuilder;
	use BunyipFormBuilder\elements\TextFormBuilder;

	include 'helpers.php';

	$form = new FormBuilder();

	$fieldset = $form->addFieldset('test', 'id', 'name');

	$attr = array(
	    'label'=>'Name',
	    'id'=>'name-id',
	    'name'=>'name',
	);
	$form->addElem(new TextFormBuilder($attr), $fieldset);
	$form->setFieldset($fieldset);
	$form->render();
  
Produces the following HTML:

.. code-block:: html

    <form class="bunyipform" action="index.php" method="post">
    <fieldset id="id" name="name">
      <legend>test</legend>
    <label for="name-id">Name</label>
    <input type="text" id="name-id" name="name" value="">
    </fieldset>
    </form>

