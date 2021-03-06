# CoverPop

CoverPop is modal splash page plugin that is easily styleable.

## Usage

If you are trying to show up a lightbox popup similar first time visitors that is easily styleable and has cookie integration, this is for you.

If you are trying to show a colorbox image when someone clicks on an internal link, this isn't for you.

## Background

CoverPop is an extension of code that [we](http://newmediacampaigns.com "New Media Campaigns") frequently found ourselves using on political campaign websites for email signups with first time visitors. We needed something that was customizable to the point we could use it exactly how we wanted and didn't get in the way.

## Questions and feature requests

Please add an issue instead of sending me an email. It makes it easier to keep track and allows other people to participate in the discussion.

## Setup

### CSS

Include the plugin css file:

```html
<link rel="stylesheet" href="css/CoverPop.css">
```

### JS

CoverPop does not use jQuery.

Include the CoverPop.js file at the bottom of your markup.

```html
<script src="js/CoverPop.js"></script>
```

Start it with the default settings:

```javascript
CoverPop.start();
```

**CoverPop** can be customized:

```javascript
CoverPop.start({
    coverId:             'CoverPop-cover',       // set default cover id
    expires:             30,                     // duration (in days) before it pops up again
    closeClassNoDefault: 'CoverPop-close',       // close if someone clicks an element with this class and prevent default action
    closeClassDefault:   'CoverPop-close-go',    // close if someone clicks an element with this class and continue default action
    openClassDefault:    'CoverPop-open',        // set class name added to HTML element when CoverPop is opened
    cookieName:          '_CoverPop',            // to change the plugin cookie name
    onPopUpOpen:         function() {},          // on popup open callback function
    onPopUpClose:        function() {},          // on popup close callback function
    forceHash:           'splash',               // hash to append to url to force display of popup (e.g. http://yourdomain.com/#splash)
    delayHash:           'go',                   // hash to append to url to delay popup for 1 day (e.g. http://yourdomain.com/#go)
    closeOnEscape:       true                    // close if the user clicks escape
    delay:               0                       // set an optional delay (in milliseconds) before showing the popup
    hideAfter:           null                    // set an optional time (in milliseconds) to autohide
});
```

### HTML

`#CoverPop-cover` is used on the full window cover.

By default, a click on any element with `.CoverPop-close` will close the popup. The plugin uses `preventDefault` with elements with this class.

If you wish to continue with the default action, but also hide the popup, add `.CoverPop-close-go`. This is particularly useful for form submissions that are sent to another page.

```html
<body>


  <!-- your site's markup -->


  <!-- start popup -->
  <div id="CoverPop-cover" class="splash">
      <div class="CoverPop-content splash-center">

          <!-- the popup content (form, welcome message, etc.) -->

          <a class="CoverPop-close" href="#">or skip signup</a>

      </div><!--end .splash-center -->
  </div><!--end .splash -->
  <!-- end popup -->

  <!-- js, etc. -->

</body>
```

## Examples

### Use a new cookie

*Example use:* You changed the popup, and want all new visitors to see the new one.

```js
CoverPop.start({
    cookieName: 'CoverPop-new'
});
```

### Manually close the popup after validation of a form

```js
if (formIsValid()) {
    CoverPop.close();
}
```

### Delay showing the popup for 4 seconds

*Example use:* You'd prefer to have the popup not show immediately, and instead wait 4 seconds.

```js
CoverPop.init({
    delay: 4000
});
```

### Hide popup after 30 seconds

*Example use:* You want the popup to hide after a set amount of time if it's still open.

```js
CoverPop.init{(
    hideAfter: 1000 * 30
)};
```

### Hide popup to the visitor for a day

*Example use:* You are sending visitors to a page that already has a signup form, and don't want them to see the popup.

```js
http://www.example.com/#go
```

### Force popup

*Example use:* You are sending visitors to a page and want visitors who have already been to the site to see the popup again.

```js
http://www.example.com/#splash
```

### Change time before cookie expires

*Example use:* You want visitors to see the popup every 7 days, instead of 30.

```js
CoverPop.start({
    expires: 7
});
```

### Do something after the popup closes

*Example use:* You want to start a video after the popup is closed.

```js
CoverPop.start({
    onPopUpClose: function() {
        var player = document.getElementById('myVideo');
        player.play();
    }
});
```

### Hide the popup when someone clicks submit on a form and continue

*Example use:* You want to close the popup and set the cookie when a visitor clicks submit on a form in the popup.

```html
<input type="submit" value="Submit" class="CoverPop-close-go">
```


## License

MIT
