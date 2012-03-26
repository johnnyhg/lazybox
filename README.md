LazyBox
=======

Lazybox is a jQuery-based, lightbox that can display entire remote pages, images and confirmation dialogs.
Replace standard rails confirmations with lazybox just added several rows to your project. Use lazybox with rails assets pipeline.

LazyBox implemented using only css and jquery without images.
This is high perfomance modal dialogs. All unpacked files take only 5 kb.
This is simplest solution for popup windows and custom confirmation dialogs.

Installing
------------

Add it to your Gemfile:

```ruby
    gem 'lazybox'
```

Then run `bundle install` to update your application's bundle.

Include in your `application.css`:

```css
    /*
     * ...
     *= require lazybox
     * ...
     */
```

And in `application.js`:

```javascript
    //= require lazybox
```

Usage
-----

###Remote pages
Usual remote link:

```ruby
  link_to 'Lazybox', new_model_path, :remote => true
```

In your controller:

```ruby
  def new
    @model = Model.new
  end

  def create
    @model = Model.new(params[:model])
    render :action => :new unless @model.save
  end
```

`new.js.haml`

```ruby
  $.lazybox("#{escape_javascript(render :partial => 'form')}");
```

`create.js.haml`

```ruby
  $.lazybox.close()
  window.location.reload()
```
![LazyBox](http://i.imgur.com/FEYpJ.png)

###Confirmations

You can replace standard rails confirmations with lazybox

And in `application.js`:

```javascript
  $.rails.allowAction = $.lazybox.confirm;
```

![LazyBox](http://i.imgur.com/1OQdU.png)

for options use global lazybox settings:

```javascript
  $.lazybox.settings = {cancelClass: "button gray", submitClass: 'button gray', overlay: false}
```

![LazyBox](http://i.imgur.com/2gW9R.png)

###Images

```ruby
  link_to 'Image', image.url, :rel => :lazybox
```
Include in your `app/assets/javascripts/application.js`:

```javascript
$(document).ready(function() {
  $('a[rel*=lazybox]').lazybox();
  // or with options
  $('a[rel*=lazybox]').lazybox({overlay: true, esc: true, close: true, modal: true, klass: 'class'});
});
```

![LazyBox](http://i.imgur.com/r6pfy.png)

If there are more than one link to image you can click on image in the lazybox to show the next one

```haml
  = link_to image.url, :rel => :lazybox do
    = image_tag image.url, :height => 100
  = link_to image2.url, :rel => :lazybox do
    = image_tag image2.url, :height => 100
```

Options
-------

    overlay:  true|false //default true. Show lazybox overlay.
    esc:      true|false //default true. Close lazybox on esc press.
    close:    true|false //default true. Show close lazybox button.
    modal:    true|false //default true. Close lazybox on overlay click.
    opacity:  0.6 //default 0.3. Set opacity for lazybox overlay.
    klass:    'class' // Set class for lazybox. <div id='lazybox' class='class'>...</div>
    //confirmation options
    cancelText: //default 'Cancel'. Cancel button text.
    submitText: //default 'Ok'. Confirm button text.
    cancelClass: //default 'button'. Cancel button class.
    submitClass: //default 'button'. Confirm button class.

Events
------

    $.lazybox.show()
    $.lazybox.close()
    $.lazybox.center()
    $(document).trigger('close.lazybox')
    $(document).trigger('center.lazybox')


Browser Compatibility
---------------------

ie7 +
Chrome
Firefox
Opera
Safari

Copyright© Alex Galushka
