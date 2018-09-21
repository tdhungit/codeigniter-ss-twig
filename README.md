# CodeIgniter Simple and Secure Twig

[![Latest Stable Version](https://poser.pugx.org/kenjis/codeigniter-ss-twig/v/stable)](https://packagist.org/packages/kenjis/codeigniter-ss-twig) [![Total Downloads](https://poser.pugx.org/kenjis/codeigniter-ss-twig/downloads)](https://packagist.org/packages/kenjis/codeigniter-ss-twig) [![Latest Unstable Version](https://poser.pugx.org/kenjis/codeigniter-ss-twig/v/unstable)](https://packagist.org/packages/kenjis/codeigniter-ss-twig) [![License](https://poser.pugx.org/kenjis/codeigniter-ss-twig/license)](https://packagist.org/packages/kenjis/codeigniter-ss-twig)

This package provides simple Twig integration for [CodeIgniter](https://github.com/bcit-ci/CodeIgniter) 3.x.

## Folder Structure

```
codeigniter/
└── application/
    └── libraries/
        └── Twig.php
```

## Requirements

* PHP 5.4.0 or later
* Twig 1.22.0 or later (Also, simply checked with Twig v2.x)

## Installation

### With Composer

* Add code below to composer.json
~~~
"require": {
    ...
    "kenjis/codeigniter-ss-twig": "dev-master"
},
"repositories": [
    ...
    {
        "type": "git",
        "url": "https://github.com/tdhungit/codeigniter-ss-twig.git"
    }
]
~~~

Install `libraries/Twig.php` to your CodeIgniter application folder:

~~~
$ php vendor/kenjis/codeigniter-ss-twig/install.php
~~~

* Above command always overwrites exisiting files.
* You must run it at CodeIgniter project root folder.

### Without Composer

Add composer.json file
~~~
{
    "require": {
        "kenjis/codeigniter-ss-twig": "dev-master"
    },
    "repositories": [
        {
            "type": "git",
            "url": "https://github.com/tdhungit/codeigniter-ss-twig.git"
        }
    ]
}
~~~

Install `libraries/Twig.php` to your CodeIgniter application folder:

~~~
$ php vendor/kenjis/codeigniter-ss-twig/install.php
~~~


Uncomment this line
~~~
require_once APPPATH . '../vendor/autoload.php';
~~~

## Usage

### Loading Twig Library

~~~php
$this->load->library('twig');
~~~

You can override the default configuration:

~~~php
$config = [
	'paths' => ['/path/to/twig/templates', VIEWPATH],
	'cache' => '/path/to/twig/cache',
];
$this->load->library('twig', $config);
~~~

### Rendering Templates

Render Twig template and output to browser:

~~~php
$this->twig->display('welcome', $data);
~~~

Above code renders `views/welcome.twig`.

> **Note:** I've changed the method name from `render()` to `display()`. Now `render()` method returns string only.

Render Twig template:

~~~php
$output = $this->twig->render('welcome', $data);
~~~

Above code renders `views/welcome.twig`.

### Adding a Global Variable

~~~php
$this->twig->addGlobal('sitename', 'My Awesome Site');
~~~

### Getting Twig_Environment Instance

~~~php
$twig = $this->twig->getTwig();
~~~

### Supported CodeIgniter Helpers

* `base_url`
* `site_url`
* `anchor`
* `form_open`
* `form_close`
* `form_error`
* `form_hidden`
* `set_value`

Some helpers are added the functionality of auto-escaping for security.

### Adding Your Functions

You can add your functions with configuration:

~~~php
$config = [
	'functions' => ['my_helper'],
	'functions_safe' => ['my_safe_helper'],
];
$this->load->library('twig', $config);
~~~

If your function explicitly outputs HTML code, you will want the raw output to be printed. In such a case, use `functions_safe`, and **you have to make sure the output of the function is XSS free**.

### Reference

#### Documentation

* http://twig.sensiolabs.org/documentation
