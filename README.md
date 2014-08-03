cakephp3-bootstrap3-helpers
===========================

CakePHP 3.0 Helpers to generate HTML with @Twitter Boostrap 3

This is the new repository for my CakePHP Bootstrap 3 Helpers (CakePHP 2.0 repository here: https://github.com/Holt59/cakephp-bootstrap3-helpers).

Installation
============

Run
`composer require holt59/cakephp3-bootstrap3-helpers:dev-master`
or add the following into your composer.json and run `composer update`.
```json
"require": {
  "holt59/cakephp3-bootstrap3-helpers": "dev-master"
}
```

Load the plugin in your bootstrap file
```php
// /config/bootstrap.php
Plugin::load('Bootstrap3');
```

How to use?
===========

Just add Helper files into your View/Helpers directory and load the helpers in you controller:
```php
public $helpers = [
    'Html' => [
        'className' => 'Bootstrap3.BootstrapHtml'
    ],
    'Form' => [
        'className' => 'Bootstrap3.BootstrapForm'
    ],
    'Paginator' => [
        'className' => 'Bootstrap3.BootstrapPaginator'
    ],
    'Modal' => [
        'className' => 'Bootstrap3.BootstrapModal'
    ]
];
```

I tried to keep CakePHP helpers style. You can find the documentation directly in the Helpers files.

Html
====

Overload of <code>getCrumbList</code> and new functions availables:

```php
$this->Html->label('My Label', 'primary') ;

$this->Html->badge('1') ;
$this->Html->badge('2') ;

$this->Html->alert('This is a warning alert!') ;
$this->Html->alert('This is a success alert!', 'success');
```

See the source for full documentation.

Form
====

Standard CakePHP code working with this helper!

```php
$this->Form->create($myModel);
$this->Form->input('field1') ;
$this->Form->input('field2') ;
$this->Form->input('field3') ;
$this->Form->end('Submit') ;
```

Added possibility to create inline and horizontal forms: `$this->Form->create($myModal, ['horizontal' => true, 'inline' => false]);`

With <code>horizontal</code>, it is possible to specify the width of each columns:
```php
$this->Form->create($myModal, [
    'horizontal' => true,
    'cols' => [ // Total is 12
        'label' => 2,
        'input' => 6,
        'error' => 4
    ]
]);
```

You can also set column widths for different screens:
```php
$this->Form->create($myModal, [
    'horizontal' => true,
    'cols' => [ 
        'sm' => [
            'label' => 4,
            'input' => 4,
            'error' => 4
        ],
        'md' => [
            'label' => 2,
            'input' => 6,
            'error' => 4
        ]
    ]
]);
```

New functions available to create buttons group, toolbar and dropdown:
```php
$this->Form->buttonGroup([$this->Form->button('1'), $this->Form->button('2')]) ;
$this->Form->buttonToolbar([
    $this->Form->buttonGroup([$this->Form->button('1'), $this->Form->button('2')]),
    $this->Form->buttonGroup([$this->Form->button('3'), $this->Form->button('4')])
]) ;
$this->Form->dropdownButton('My Dropdown', [
    $this->Html->link('Link 1'),
    $this->Html->link('Link 2'),
    'divider',
    $this->Html->link('Link 3')
]);
```

New options available when creating input to prepend / append button or text to input:
```php
$this->Form->input('mail', [
    'prepend' => '@', 
    'append' => $this->Form->button('Send')
]) ;
$this->Form->input('mail', [
    'append' => [
        $this->Form->button('Button'),
        $this->Form->dropdownButton('Dropdown', [
            'A', 'B', 'divider', 'C'
        ]);
    ]
]) ;
```

It is possible to specify default button type and column width (for horizontal forms) when creating the helper:
```php
// In your Controller
public $helpers = [
    'Form' => [
        'className' => 'Bootstrap3.BootstrapForm',
        'buttons' => [
            'type' => 'primary'
        ],
        'columns' => [
            'sm' => [
                'label' => 4,
                'input' => 4,
                'error' => 4
            ],
            'md' => [
                'label' => 2,
                'input' => 6,
                'error' => 4
            ]
        ]
    ]
];
```

Modal
=====

Simple helper to create modal, 3 ways of using it:

**First one (simple) - You should use this one if possible!**

```php
<?php
// Start a modal with a title, default value for 'close' is true
echo $this->Modal->create("My Modal Form", ['id' => 'MyModal', 'close' => false]) ; 
?>
<p>Here I write the body of my modal !</p>
<?php
// Close the modal, output a footer with a 'close' button
echo $this->Modal->end() ;
// It is possible to specify custom buttons:
echo $this->Modal->end([
    $this->Form->button('Submit', ['bootstrap-type' => 'primary']),   
    $this->Form->button('Close', ['data-dismiss' => 'modal']) 
]);
?>
```

**Second one - No HTML, the various section are split in different methods.**
```php
<?php
echo $this->Modal->create(['id' => 'MyModal2']) ;
echo $this->Modal->header('My Title', ['close' => false]) ; 
echo $this->Modal->body('My Body', ['class' => 'my-body-class']) ;
echo $this->Modal->footer([
    $this->Form->button('Submit', ['bootstrap-type' => 'primary']),   
    $this->Form->button('Close', ['data-dismiss' => 'modal']) 
]) ;
echo $this->Modal->end() ;
?>
```

**Third one (advanced) - You start each section manually, but you can customize almost everything!**
```php
<?php
echo $this->Modal->create(['id' => 'MyModal3']) ;
echo $this->Modal->header(['class' => 'my-header-class']) ; 
?>
<h4>My Header!</h4>
<?php
echo $this->Modal->body() ;
?>
<p>My body!</p>
<?php
echo $this->Modal->footer(['close' => false]) ;
?>
<p>My footer... Oops, no buttons!</p>
<?php
echo $this->Modal->end() ;
?>
```

With the two last versions, it is possible to omit a part:
```
<?php
echo $this->Modal->create() ;
echo $this->Modal->body() ; // No header
echo $this->Modal->footer() ; // Footer with close button (default)
echo $this->Modal->end() ;
?>

**Info:** You can use the `BootstrapFormHelper` to create toggle button for your modals!

```php
echo $this->Form->button('Toggle Form', ['data-toggle' => 'modal', 'data-target' => '#MyModal']) ;
```

Copyright and license
=====================

Copyright 2013 Mikaël Capelle.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this work except in compliance with the License. You may obtain a copy of the License in the LICENSE file, or at:

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
