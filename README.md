# Fluent Stacker for PHP
Stacker is an open source library for building responsive email notifications with minimal markup. It's great for generating user notifications like password resets, user welcomes, receipts, shipping notifications etc. No views required.

## Benefits ##
- Easy API to generate HTML based e-mail bodies in your app
- Cleaner code base with less markup and no views required
- Less time wrestling with CSS inlining
- Responsive out of the box

![Mockup](https://github.com/fivesqrd/fluent-stacker-php/blob/1.0/docs/mockups/Responsive-Devices-Website.png "Responsive layout")

## Live Demo ##

To see a real sample in your inbox, head on over to http://fluentmsg.com and send a test email to yourself.

## Design ##

Baked into the Stacker library is a responsive HTML layout and markup various reusable UI components. Currently this repo includes a beautiful minimal theme called [Musimal](https://github.com/fivesqrd/musimal). We hope to add more in the near future.

## UI Compents ##
Fluent provides a single column responsive email layout with support for several types of UI components. By combining the various UI components together, one can easily generate many of the most common types of user notifications needed for a project. Each component occupies the full width of the layout and is stacked on top of each other. 


The current supported UI components are:
1. Teaser - a short piece of text displayed on the list of view of most email clients
2. Logo - image displayed at the top of a message
3. Title - heading inside the message body
4. Paragraphs - sections of text seperated by decent helping of space
5. Numbers - highlight a numeric value with a caption
6. Buttons - call to action button
7. Segments - custom HTML to be displayed
8. Footer - a line of text at the bottom for an address, opt out, etc

## Sample Email Layout ##
Below is a sample of an email layout that uses some of the UI components
![Layout](https://github.com/fivesqrd/fluent-stacker-php/blob/1.0/docs/mockups/Layout-640x960.png "Responsive e-mail layout")

## Install ##
```
php composer.phar require fluent/stacker:1.0
```

For Laravel projects there is an easy to install package available here: https://github.com/Five-Squared/Fluent-Laravel


## Quick Examples ##
Create a responsive HTML message body:
```
$html = (new Fluent\Layout())->create()
    ->title('My little pony')
    ->paragraph('Lorem ipsum dolor sit amet, consectetur adipiscing elit.')
    ->number(['caption' => 'Today', value => date('j M Y')])
    ->button('http://www.mypony.com', 'Like my pony')
    ->paragraph('Pellentesque habitant morbi tristique senectus et netus et malesuada fames.')
    ->render();

sendmail();
```

## Using Fluent Server Features ##
Although Stacker can render HTML completely on its own. It also alo possible to couple it with Fluent Server to add some advanced features. 
Fluent Server is a web service that makes email delivery simple and provides a bunch of other helpful features.

To make use of these features, you'll need a Fluent Server account and the Fluent Client:
```
php composer.phar require fluent/client:4.0
```

Once the Fluent Client is in place, the following extra methods will become available:
### Double action: Create and send ###
Create and send expressively:
```
$messageId = (new Fluent\Layout())->create()
    ->title('My little pony')
    ->paragraph('Lorem ipsum dolor sit amet, consectetur adipiscing elit.')
    ->send([
        'subject'   => 'Testing it', 
        'recipient' => 'user@theirdomain.com', 
        'sender'    => 'me@myapp.com'
    ]);
```

Create and send expressively:
```
$messageId = (new Fluent\Message())->create()
    ->title('My little pony')
    ->paragraph('Lorem ipsum dolor sit amet, consectetur adipiscing elit.')
    ->deliver()
    ->subject('Testing it')
    ->header('Reply-To', 'me@myapp.com')
    ->from('me@myapp.com', 'My App')
    ->to('user@theirdomain.com')
    ->send(); ;
```
