Joi provides an expressive api for describing JSON schema, and can be added directly to hapi routes via the ```validate``` portion of a route's configuration.

Joi schema are created by creating an object containing matching key:description pairs. For example: 

```javascript

var Joi = require('joi');

var schema = {
  name: Joi.string().required(),
  year: Joi.number()
};

```

Joi provides a number of built-in objects, like ```string```, and ```number``` above. It also provides ```object```, ```date```, ```array```. Some types even provide commonly used objects, like this:

```javascript
var Joi = require('joi');

var schema = {
  email: Joi.string().email(),
  amex: Joi.string().creditcard(),
  token: Joi.string().alphanum()
};
```

In addition to types, there are ways to add logic to your schema. Strings and arrays can be checked for length, numbers can be assigned range values, and even given logical operators like ```with``` and ```xor```. 

```javascript
var Joi = require('joi');

//logical operators are tied to an object, hence the functions chained at the end.
var schema = {
  email: Joi.string().email(),
  mobile: Joi.string(),
  firstName: Joi.string(),
  lastName: Joi.string()
}.xor('email', 'mobile') //xor will make sure there is only one of the options passed in as a parameter
.with('firstName', 'lastName');  //with takes two values, 'key' (string) and 'peers' (string or array of strings)
```
For this exercise, create a server that contains a ```POST``` endpoint that only accepts a JSON object that matches the following rules: 

1. 'isGuest' is required boolean, and if it's false a string 'username' is required. 
2. 'password' is alphanumeric, and should only be there if 'accessToken' isn't available.
3. Any additional parameters should be allowed, but not checked

Ultimately, the schema object should resemble this, but with Joi types:

```javascript
var schema = {
  isGuest://boolean,
  username://string,
  accessToken://alphanumeric,
  password://alphanumeric
};
```

-----------------------------------------------------------------
##HINTS

A route can have a config with a 'validate' key that specifies the validation rules for that route, like this:





The API docs contain more information about (Routes)[`http://hapijs.com/api#route-configuration`], and (Joi)['https://github.com/hapijs/joi/blob/master/README.md']