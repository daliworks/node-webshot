# node-webshot

Webshot provides a simple API for taking webpage screenshots. The module is a light
wrapper around PhantomJS, which utilizes WebKit to perform the page rendering. 

## Examples
A simple example:

```javascript
var webshot = require('webshot');

webshot('google.com', 'google.png', function(err) {
  // screenshot now saved to google.png 
});
```

An example showing how to take a screenshot of a site's mobile version:

```javascript
var webshot = require('webshot');

var options = {
  screenSize: {
    width: 320
  , height: 480
  }
, shotSize: {
    width: 320
  , height: 'all'
  }
, userAgent: 'Mozilla/5.0 (iPhone; U; CPU iPhone OS 3_2 like Mac OS X; en-us)'
    + ' AppleWebKit/531.21.20 (KHTML, like Gecko) Mobile/7B298g'
}

webshot('flickr.com', 'flickr.jpeg', options, function(err) {
  // screenshot now saved to flickr.jpeg
});
```

## Installation
This module uses PhantomJS to render pages. Make sure Phantom is present on 
your system. It must either be available through the `$PATH` variable or have its 
location given by the `phantomPath` option (see following section).

## Options
An optional `options` object can be passed as the third parameter in a call to webshot.

<table>
  <thead>
    <tr>
      <th>Option</th>
      <th>Default Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>screenSize</th> 
      <td>
<pre>{ width: 1024
, height: 768 }</pre>
      </td>
      <td>The dimensions of the browser window</td> 
    </tr>
    <tr>
      <th>shotSize</th> 
      <td>
<pre>{ width: 'screen'
, height: 'screen' }</pre>
      </td>
      <td>The area of the page document, starting at the upper left corner, to render.
      Possible values are 'screen', 'all', and a number defining a pixel length. 
      <br /> <br />
      <strong>'screen'</strong> causes the length to be set to the length of the window (i.e. 
      the shot displays what is initially visible within the browser window).
      <br /> <br />
      <strong>'all'</strong> causes the length to be set to the length of the document along
      the given dimension. </td> 
    </tr>
    <tr>
      <th>phantomPath</th> 
      <td>'phantomjs'</td>
      <td>The location of phantomjs. By default, webshot assumes it is accessible through
      the <code>$PATH</code> variable. </td> 
    </tr>
    <tr>
      <th>userAgent</th> 
      <td>undefined</td>
      <td>The <code>user-agent</code> string Phantom sends to the requested page. If left unset, the default
      Phantom <code>user-agent</code> will be used</td> 
    </tr>
    <tr>
      <th>script</th> 
      <td>undefined</td>
      <td>An arbitrary function to be executed on the requested page. The script executes within the page's 
      context and can be used to modify the page before a screenshot is taken. 
      </td> 
    </tr>
  </tbody>
</table>

## Tests
Tests are written with [Mocha](http://visionmedia.github.com/mocha/) and can be run with `npm test`.