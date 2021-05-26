# Integration of SMSLink - SMS Gateway (HTTP) using [Composer](https://getcomposer.org/) (Dependency Manager for PHP) 

This is an integration example for sending SMS using [SMSLink.ro](https://www.smslink.ro) API, called [SMS Gateway](https://www.smslink.ro/sms-gateway.html). 
SMSLink.ro allows you to send SMS to all mobile networks in Romania and also to more than 168 countries and more than 1000 mobile operators worldwide. 

## Installation

Using [Composer](https://getcomposer.org/) (Dependency Manager for PHP) 

``` bash
$ composer require smslink/smsgateway
```

[smslink/smsgateway](https://packagist.org/packages/smslink/smsgateway) Package on Packagist - The PHP Package Repository

## Requirements

1. Create an account on [SMSLink.ro](https://www.smslink.ro/inregistrare/)
2. Create a SMS Gateway connection at [SMSLink.ro / SMS Gateway / Configuration & Settings](https://www.smslink.ro/sms/gateway/setup.php). Each SMS Gateway connection is a pair of Connection ID and Password. 

## Supported Functions

1. *$Connection->sendMessage()* - sends an SMS
2. *$Connection->accountBalance()* - retrieve SMSLink account balance

## Features

1. Supports HTTP and HTTPS protocols
2. Supports PHP cURL GET, PHP cURL POST and file_get_contents()
 
## System Requirements 

* PHP 5 or greater with CURL enabled or file_get_contents with allow_url_fopen to be set to 1 in php.ini  
* [Composer](https://getcomposer.org/) - Dependency Manager for PHP
* [smslink/smsgateway](https://packagist.org/packages/smslink/smsgateway) Package on Packagist - The PHP Package Repository

## Usage Example using Composer

``` php
<?php

/*
 *
 *     Require Autoload (change autoload.php path to match your project)
 *       
 */
require_once 'vendor/autoload.php';

/*
 *
 *     Include the SMSLink\SMSGateway\Connection namespace
 *       
 */

use SMSLink\SMSGateway\Connection;

/*
 * 
 * 
 *     Initialize SMS Gateway     
 *     
 *       Get your SMSLink / SMS Gateway Connection ID and Password from 
 *       https://www.smslink.ro/get-api-key/
 *       
 *       
 *       
 */

$Connection = new Connection();

$Connection->setConnectionCredentials("MyConnectionID", "MyConnectionPassword");

/*
 *     Sets the method in which the parameters are sent to SMS Gateway
 *
 *      1 for cURL GET  (make sure you have PHP cURL installed) (default and recommended)
 *      2 for cURL POST (make sure you have PHP cURL installed) 
 *      3 for file_get_contents (requires allow_url_fopen to be set to 1 in php.ini) 
 *           (recommended if you do not have PHP cURL installed)
 */
$Connection->setRequestMethod(1);      

/*
 *     Sets the protocol that will be used by SMS Gateway (HTTPS or HTTP).
 */
$Connection->setProtocol("HTTPS");

/*
 *     Display account balance before sending SMS
 */
$accountBalance = $Connection->accountBalance();

echo "My Account Balance is: ".$accountBalance["national-SMS"]." national SMS, ".
          $accountBalance["international-SMS"]." national SMS<br />";

/*
 *     Sends SMS #1
 */
$messageId = $Connection->sendMessage("07xyzzzzzz", "My first hello world message.");

if ($messageId == false) echo "Message sent failed. Log: ".$Connection->getLastLogMessage().".<br />"; 
     else echo "Message successfully sent with ID: ".$messageId.".<br />";

/*
 *     Sends SMS #2
 */
$messageId = $Connection->sendMessage("07xyzzzzzz", "My second hello world message.");

if ($messageId == false) echo "Message sent failed. Log: ".$Connection->getLastLogMessage().".<br />";
    else echo "Message successfully sent with ID: ".$messageId.".<br />";

/*
 *     Display account balance after sending SMS
 */
$accountBalance = $Connection->accountBalance();

echo "My Account Balance is: ".$accountBalance["national-SMS"]." national SMS, ".
          $accountBalance["international-SMS"]." national SMS<br />";

/*
 *     Display the communication log with SMSLink
*/
$Connection->displayLogMessages();

?> 
```

## Usage Example without using Composer

[SMSLink.ro](https://www.smslink.ro) [SMS Gateway](https://www.smslink.ro/sms-gateway.html) can also be used without Composer. For using SMSLink SMS Gateway without Composer see [the following example](https://github.com/SMSLink-ro/Integration-example-of-SMS-Gateway-HTTP-using-PHP).

## Documentation

The [complete documentation](https://www.smslink.ro/sms-gateway-documentatie-sms-gateway.html) of the SMSLink - SMS Gateway API can be found [here](https://www.smslink.ro/sms-gateway-documentatie-sms-gateway.html), describing all available APIs (HTTP GET / POST, SOAP / WSDL, JSON and more).

## Additional modules and integrations

SMSLink also provides modules for major eCommerce platforms (on-premise & on-demand), integrations using Microsoft Power Automate, Zapier or Integromat and many other useful features. Read more about all available features [here](https://www.smslink.ro/sms-gateway.html). 

## Support

For technical support inquiries contact us at contact@smslink.ro or by using any other available method described [here](https://www.smslink.ro/contact.php).
