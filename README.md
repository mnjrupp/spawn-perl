spawn-perl
==========
A CGI webserver for perl. Great for use if you don't have access to Apache or IIS environment.
 A quick script for development purposes.

## Usage in Node and express

```js
var Perlcgi = require('./spawn-perl').spawnPerlCGI;
var express = require('express')
  ,http = require('http')
  ,url = require('url')
  ,path = require('path');
var app = express();
var script_name = '/cgi-bin/guest.cgi';

var script = path.join(__dirname, '/cgi-bin/guest.cgi');

  app.set('port', process.env.PORT || 3000);


app.get(script_name, function(req, res){
      var perl = new Perlcgi(script,req,null,function(err,data){
       
       
                 
			   if(err){
                console.log(err);
				}
             
                 res.header(perl.getHeader());
                 res.write(data);
                 res.end();
				});                    
   });

app.post(script_name, function(req, res){
       var perl = new Perlcgi(script,req,null,function(err,data){
		 
       if(err){              
                console.log(err);
				}                
                 res.header(perl.getHeader());
                 res.write(data);
                 res.end();
       });
   });
 
http.createServer(app).listen(app.get('port'), function(){
  console.log("Express server listening on port " + app.get('port'));
});
```
To use the example app.js, make sure you install express.The package.json is included
```
   $ cd src
   $ npm install
``` 
## Features
 
  * CGI Environment created for you, or you can pass own %ENV in the 3rd parameter
  * The CGI header is removed from the stdout of the Perl script, so you can pass own header in using the express
    framework, or you can use the CGI header by calling the getHeader() method and passing as parameter in response.header()
  * Tested with both Windows, using Strawberry Perl, and UBuntu.
