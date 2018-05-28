# MutyurPHPMVC
Minimalist PHP framework 

# Setup config.php

You can find a config.php in the application folder.

## Set base_url

You have to set base_url to where you can access the index.php on your web server. 

For example if you using the PHP's embed web server for development:

````
php -S 127.0.0.1:8001          <- if you navigated to index.php's folder.
````

```php
/** @brief system's settings*/
$config['system']=array(
	'baseurl' => 'http://127.0.0.1:8001/',
```
If you using this settings you can call the web page on 

```
http://127.0.0.1:8001/index.php or http://127.0.0.1:8001/ 
```
## Setting up sesshandler extension

- sessionpath - the path of session folder
- sessiontimeout - session timeout in milliseconds
- sessiontype - it can be only 'file' currently
- sessionencryptionkey - if you want to save session data in enrypted format you can set the key here (32 byte) 
- sessionencryptionnonce - nonce's length is 24 for libsodium extension

## Routing

```php
/** @brief routes*/
$config['routes']=array(
	'default' => 'defaultcontroller/index',	
	'test' => 'defaultcontroller/test'		
);	
```

The http://127.0.0.1:8001 or http://127.0.0.1:8001/index.php or http://127.0.0.1:8001/default calling the application/controllers/defaultcontroller.php->index function.
The http://127.0.0.1:8001/test or http://127.0.0.1:8001/index.php/test calling the application/controllers/defaultcontroller.php->test function.

# Language handling

## Setting up default language in config.php

```
/** @brief languages*/
$config['languages']=array( // for languagehandler extension
	'default' => 'english', 
);
```
## Load language extension
```
$this->m_lang=$this->load_extension('languagehandler');
```
## Set and get language 
```
$this->m_lang->set_language('english');

$langname=$this->m_lang->get_language();
```
## Get language item

```
$this->m_lang->set_language('english');
$this->m_lang->get_item('caption');
```
## Language file in application/languages
- Separated files by language
- Key => value structure
For example:
```
<?php

if (! defined ( 'mutyurphpmvc_inited' ))
	exit ( 'No direct script access allowed' );

$lang['english']=array(
	'caption' => 'Mütyür PHP MVC sample page',
	.
	.
	.
);	
```





