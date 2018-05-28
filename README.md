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

```
/** @brief system's settings*/
$config['system']=array(
	'baseurl' => 'http://127.0.0.1:8001/',
```
I you using this settings you can call the web page on 

```
http://127.0.0.1:8001/index.php or http://127.0.0.1:8001/ 
```
