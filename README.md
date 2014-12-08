# SevenSegmentsApi

Implementation of json tracking api for [7segments](http://7segments.com). 

## Installation

Sources are readily aviable, as well as an exported unitypackage in the rot of this repository.

## Usage

### Basic Interface

To start tracking, you need to know the uri of your 7segments api instance, usualy ```https://api.7segments.com/```, your ```company_token``` and generate a unique ```customer_id``` for the customer you are about to track. The unique ```customer_id``` can either be string, or an object representing the ```customer_ids``` as referenced in [the api guide](https://docs.7segments.com/technical-guide/integration-rest-client-api/#Detailed_key_descriptions).
Setting ```customer_id = "123-asdf"``` is equivalent to ```customer_id = new Dictionary<String, String> () {{"registered","123-adf"}};```


```
var sevenSegments = new  SevenSegments (company_token,server_uri,customer_id);
```

If this is the beginning of tracking of a new user, you need to first ```Identify``` him against the server.

All of the commands spawn a coroutine, so that they won't block the processing in your main application.

```
sevenSegments.Identify (customer_id, new Dictionary<String, Object> () {{"email","asdf@asdf.com"}});
```

For serialization we utilize small embedded MiniJSON parser. 

You track various events by utilizing the Track function.
It assumes you want to track the customer you identified by ```Identify```.
The only required field is a string describing the type of your event.
By default the time of the event is tracked as the epoch time,
and diffed against the server time of 7segments before sending.

```
sevenSegments.Track ("login");
```
