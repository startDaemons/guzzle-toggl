guzzle-toggl
============

A Toggl API client based on Guzzle PHP

## Installation

The library is available through Composer, so its easy to get it. 
Simply add this to your `composer.json` file:

    "require": {
        "ajt/guzzle-toggl": "dev-master"
    }
    
And run `composer install`

## Features

* supports version 6 API with API Key authentication
* supports version 8 API with API Key authentication

## Todo

- [ ] Complete the service description for v6
- [ ] Complete the service description for v8
- [ ] Add some examples
- [ ] Add tests
- [ ] Add some Response models

## Usage
    
To use the Toggl API Client simply instantiate the client with the api key.
More information on the key available at https://www.toggl.com/public/api#api_token

```php
<?php

require dirname(__FILE__).'/../vendor/autoload.php';

use AJT\Toggl\TogglClient;
$toggl_token = ''; // Fill in your token here
$toggl_client = TogglClient::factory(array('api_key' => $toggl_token)); // Defaults to the v6 api

// If you want the v8 api, add an api version to the client
$toggl_client = TogglClient::factory(array('api_key' => $toggl_api_key, 'apiVersion' => 'v8'));

// if you want to see what is happening, add debug => true to the factory call
$toggl_client = TogglClient::factory(array('api_key' => $toggl_token, 'debug' => true)); 
```

Invoke Commands using our `__call` method (auto-complete phpDocs are included)

```php
<?php 

$toggl_client = TogglClient::factory(array('api_key' => $toggl_token));

$workspaces = $toggl_client->getWorkspaces(array());

foreach($workspaces as $workspace){
	$id = $workspace['id'];
	print $workspace['name'] . "\n";
}
``` 

Or Use the `getCommand` method (in this case you need to work with the $response['data'] array:

```php
<?php 

$toggl_client = TogglClient::factory(array('api_key' => $toggl_token));

//Retrieve the Command from Guzzle
$command = $toggl_client->getCommand('GetWorkspaces', array());
$command->prepare();

$response = $command->execute();

$workspaces = $response['data'];

foreach($workspaces as $workspace){
	$id = $workspace['id'];
	print $workspace['name'] . "\n";
}
```

## Examples
Copy the apikey-dist.php to apikey.php (in the root directory) and add your apikey.
Change the apiversion if you want. Version 6 will be removed on September 1st 2013 by Toggl
Afterwards you can execute the examples in the examples directory. 

You can look at the services.json for details on what methods are available and what parameters are available to call them

## Contributions welcome

Found a bug, open an issue, preferably with the debug output and what you did. 
Bugfix? Open a Pull Request and i'll look into it. 

## License

The Toggl API client is available under an MIT License.
