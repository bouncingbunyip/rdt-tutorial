Usage
=====

.. _installation:

Installation
------------

To use BunyipFormBuilder, first fork or download it from Github.

Then place the files somewhere in your project.

Basic Usage
----------------

To create a simple login form we will have code something like the following:

.. code-block:: php

   require_once '../Autoloader.php';
   use BunyipFormBuilder\FormBuilder;
   use BunyipFormBuilder\decorators\HintDecorator;
   use BunyipFormBuilder\elements\SubmitFormBuilder;
   use BunyipFormBuilder\elements\TextFormBuilder;
   use BunyipFormBuilder\elements\PasswordFormBuilder;
   use BunyipFormBuilder\elements\HiddenCsrfFormBuilder;

   $attr = array(
       'action'=>'echo.php',
       'method'=>'post',
       'id'=>'name-id',
       'name'=>'name'
   );

   $form = new FormBuilder($attr);
   $attributes = array('class'=>'hint--right', 'trigger'=>'Hint', 'text'=> 'This is the tooltip text');
   $tooltip = new HintDecorator($attributes);

   $fieldset = $form->addFieldset('Log In', 'id', 'name');

   $attr = array(
       'label'=>'Username',
       'id'=>'username',
       'name'=>'username',
       'tooltip'=>$tooltip
   );
   $form->addElem(new TextFormBuilder($attr), $fieldset);

   $attr = array(
       'label'=>'Password',
       'id'=>'password',
       'name'=>'password'
   );
   $form->addElem(new PasswordFormBuilder($attr), $fieldset);

   $attr = array(
       'value'=>FormBuilder::getCsrf(),
       'id'=>FormBuilder::VICSRF,
       'name'=>FormBuilder::VICSRF
   );
   $form->addElem(new HiddenCsrfFormBuilder($attr));

   $attr = array(
       'value'=>'Submit',
       'id'=>'name-id',
       'name'=>'name'
   );
   $form->addElem(new SubmitFormBuilder($attr));

   $form->setFieldset($fieldset);
   $form->render();

Produces the following HTML:

.. code-block:: html

   <link href="https://unpkg.com/hint.css@2.7.0/hint.min.css" media="screen" rel="stylesheet" type="text/css" />
   <form class="bunyipform" action="echo.php" id="name-id" method="post" name="name">
   <fieldset id="id" name="name">
     <legend>Log In</legend>
   <label for="username">Username</label>
   <input type="text" id="username" name="username" value="">
   <div class="hint--right" aria-label="This is the tooltip text">Hint</div>
   <label for="password">Password</label>
   <input type="password" id="password" name="password" value="">
   </fieldset>
   <input type="hidden" id="vicsrf" name="vicsrf" value="HwNfdAKmVvQQD3Yt">
   <input type="submit" name="name" value="Submit">
   </form>

Why would anybody do this?  That is way more PHP code than the resulting HTML.  And that is correct.

What this allows us to do is separate the logic of the form, ie which form fields and what kinds of form fields from the HTML display of the form.
I can keep the problems associated with HTML and the various browsers separate from my business logic.
As an added benefit, if I need to change the structure of the resulting HTML form, I can change (or create a new) Template file.  For example if I wanted to use Bootstrap, I can create Bootstrap specific Template files and the resulting HTML form is Bootstrapped. To change the Template file associated with a form element all I need to do is call ``$form->setTemplate('NameOfAlternativeTemplateClass');``

Additionally, I can save the HTML form to a variable and either write that into a file or use it in Front End testing, without having to spin up a headless browser like Chromium.
