###What to Use Joi for and When to Use It  

Joi is an object schema description language and validator for JavaScript objects. If you're wondering why you would need to validate JavaScript Objects, this document will give you a brief introduction on why data validation is needed and its applications. Let’s say for example, you have a web form that ask users to input their username, password, date of birth, and email. How would you prevent users from inputting gibberish into your form? You wouldn’t want to deal with submissions that are meaningless or missing parts of data. This is where data validation comes into play. Joi allows for constraints to be placed on JavaScript Object properties. Lets take a look at a simple example:
```
var Joi = require('joi');

var schema = Joi.object().keys({
    username: Joi.string().alphanum().min(5).max(25).required(),
    password: Joi.string().regex(/^[a-zA-Z0-9]{3,30}$/).required(),
    birthyear: Joi.number().integer().min(1900).max(2010),
    email: Joi.string().email()
}).with('username', 'birthyear');

Joi.validate({ username: 'abc', birthyear: 1994 }, schema, function (err, value) { });  // err === null -> valid
```
The constraints placed on each property is defined as follows:   
`username: Joi.string().alphanum().min(5).max(25).required()`
* Is required
* Must be a string
* Must contain only alphanumeric characters
* Must have a minimum of 5 characters and a maximum of 25 characters

`password: Joi.string().regex(/^[a-zA-Z0-9]{3,30}$/).required()`
* Is required
* Must be a string
* Must satisfy the custom regex

`birthyear: Joi.number().integer().min(1900).max(2010)`
* Must be a integer
* Value must be between 1900 and 2010

`email: Joi.string().email()`
* Must be a valid email address

Objects can then be evaluated using the following:
`Joi.validate( object, schema, function (err, value) {})`
* `object`: the object to be evaluated
* `schema`: the schema the object is evaluated against
* `function (err, value) {}`: returns the value if it passes or returns an error

Example:
`Joi.validate({ username: 'abc', birthyear: 1994 }, schema, function (err, value) { });  // err === null -> valid`

