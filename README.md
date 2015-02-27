# Hello DIDevs,
Grab a quick copy of AIT gateway for PHP right here and 
bootstrap your bulk SMS features

<a href="https://github.com/DeveintLabs/AfricaIsTalkingSMSGatewayPHP/archive/master.zip">Download PHP Bulk SMS Library</a>

# Setting up
Once you have your local copy, extract it to an accessible location and 
require it once. For CI, you can place it in libraries and load it with
```php
$this->load->library('GateWayFileName', $constructorConfiguration)
```
or place it in application/thirdparty then require it manually at the top of your controller
```php
require('application/thirdparty/GateWayFileName.php');

# And later instantiate it in your controller method
$gateway = new AfricasTalkingGateway($AITUsername, $AITAPIKey);
```

And you are done. Below is a sample code snippet for sending SMS. You can also grab it 
on the AIT website <a href="https://www.africastalking.com/tutorials/sms/sending/php">at this link</a>

```php
// Be sure to include the file you've just downloaded
require_once('AfricasTalkingGateway.php');

// Specify your login credentials
$username   = "MyAfricasTalkingUsername";
$apikey     = "MyAfricasTalkingAPIKey";

// Specify the numbers that you want to send to in a comma-separated list
// Please ensure you include the country code (+254 for Kenya in this case)
$recipients = "+254711XXXYYYZZZ,+254733XXXYYYZZZ";

// And of course we want our recipients to know what we really do
$message    = "I'm a lumberjack and its ok, I sleep all night and I work all day";

// Create a new instance of our awesome gateway class
$gateway    = new AfricasTalkingGateway($username, $apikey);

// Any gateway errors will be captured by our custom Exception class below, 
// so wrap the call in a try-catch block
try 
{ 
  // Thats it, hit send and we'll take care of the rest. 
  $results = $gateway->sendMessage($recipients, $message);
  foreach($results as $result) {
    // Note that only the Status "Success" means the message was sent
    echo " Number: " .$result->number;
    echo " Status: " .$result->status;
    echo " MessageId: " .$result->messageId;
    echo " Cost: "   .$result->cost."\n";
  }
}
catch ( AfricasTalkingGatewayException $e )
{
  echo "Encountered an error while sending: ".$e->getMessage();
}

// DONE!!! 
```
	


