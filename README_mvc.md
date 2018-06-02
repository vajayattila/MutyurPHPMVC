# MutyurPHPMVC
Minimalist PHP framework 

# Setup config.php

You can find the config.php in the application folder.

## Set base_url

You have to set base_url to where you can access the index.php on your web server. 

For example if you are using the PHP's embed web server for development:

````
php -S 127.0.0.1:8001          <- if you have navigated to index.php's folder.
````

```php
/** @brief system's settings*/
$config['system']=array(
	'baseurl' => 'http://127.0.0.1:8001/',
```
If you are using this settings you can call the web page on 

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

```php
/** @brief languages*/
$config['languages']=array( // for languagehandler extension
	'default' => 'english', 
);
```
## Load language extension
```php
$this->m_lang=$this->load_extension('languagehandler');
```
## Set and get language 
```php
$this->m_lang->set_language('english');

$langname=$this->m_lang->get_language();
```
## Get language item

```php
$this->m_lang->set_language('english');
$this->m_lang->get_item('caption');
```
## Language file in application/languages
- Separated files by language
- Key => value structure
For example:
```php
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
# Query parameters 
## Get request method
```php
public function test(){
	echo 'Test is works!<br>'; 
	echo $this->get_request_method().'<br>'; /* Which request method was used to access the page; i.e. 
	'GET', 'HEAD', 'POST', 'PUT'. */
}
```
## Get query parameters
```php
public function test(){
	.
	.
	print_r($this->get_query_parameters());
}
```
For example if you call 127.0.0.1:8001/test?xxx=1 then your output is will:
```php
Array ( [0] => Array ( [name] => xxx [value] => 1 ) ) 
```
## Get query parameter by keyname
```php
public function test(){
	$params=$this->get_query_parameters(); 
	print_r($params);
	echo '<br>';
	if(is_array($params)&&0<sizeof($params)){
		foreach($params as $item){
			$name=$item['name'];
			echo $name."=>".$this->get_query_parameter($name).'<br>';
		}
	}
}
```
For example if you call 127.0.0.1:8001/test?xxx=1 then your output is will:
```
xxx=1
```
# Session handling

## Loading session extension
```php
$m_session=$this->load_extension('sesshandler');
```
## Setting a session value
```php
$m_session->set('name', 'value');
```
## Getting a session value
```php
$value=$m_session->get('name');
```
## Unset a session value
```php
$m_session->uset('name');
```
# Logging
## Setting logging in config.php
```php
/** @brief logger's settings*/
$config['logger']=array(
	'error' => true,
	'warning' => true,
	'info' => true,
	'system' => true,
	'requestinfo' => true, 
	'debug' => true,
	'session' => true, // for sesshandler extension
);
```
## Write to log 
```php
// you can use everywhere 
$this->log_message('info', "Hello World!");
```
## Structure of a log file
The log file will be written separated by date in application/log folder.
```php
ERROR       - 2018-05-28 16:20:14 --> The index controller is not set in config.php.
type of logentry - date and time --> Message
```
## Define own log entry type
```php
// define type in config.php 
$config['logger']=array(
	.
	.
	.
	'my_log_type' => true, // if true then my_log_type entries will be show in log file. 
	);
	
// Using
$this->log_message('my_log_type', "Message with my_log_type type.");
```
