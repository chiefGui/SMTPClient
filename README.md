SMTP Client [![Build Status](https://travis-ci.org/andreyknupp/SMTPClient.png?branch=master)](https://travis-ci.org/andreyknupp/SMTPClient)
===========
Just a powerful *Service Mail Transfer Protocol* (SMTP) client to send mail messages.
*"This is a specific mate to send mail messages over SMTP. It isn't a universal mailer that cover all methods for sending an email*"

How it works
---------------------------
In a simple and robustly way, you could send mail messages using SMTP servers.

The first thing you need to do is to create a connection, and then perform authentication for the user. After that, send the message and you are done.

Firstly, we need a SMTP server. In this case, we'll use the Gmail server. 

Using the settings from "Outgoing Mail (SMTP) Server" from [Google](https://support.google.com/mail/answer/13287), 
we'll perform the connection and authentication for the user:

```PHP
<?php

require_once "config/bootstrap.php";

use utils\net\SMTP\Client; // SMTP client
use utils\net\SMTP\Client\Authentication\Login; // authentication mechanism
use utils\net\SMTP\Client\Connection\SSLConnection; // the connection
use utils\net\SMTP\Message; // the message

$client = new Client(new SSLConnection("smtp.gmail.com", 465));
$client->authenticate(new Login("user@gmail.com", "pswd"));
```

With that, we're connected and probably authenticated (if you replaced the **user@gmail.com** and **pswd** with valid credentials, you are good to go).

Then, just send the message:
```PHP
$message = new Message();
$message->from("user@gmail.com") // sender
        ->to("other-user@domain.com") // receiver
        ->subject("Hello") // message subject
        ->body("Hello World"); // message content

echo $client->send($message) ? "Message sent" : "Opz";
```

If the message is sent, be happy! Otherwise, if you cannot identify the kind of your problem (e.g: credentials, connection [host, port]), you can open an issue [here](https://github.com/andreyknupp/SMTPClient/issues/new).

How could I use it/test it?
----------------------
Firstly, clone the repository through:
```bash
$ git clone git://github.com/andreyknupp/SMTPClient.git
$ cd SMTPClient/
```
Switch the current directory to SMTPClient directory:
```bash
$ cd SMTPClient/
```
Install dependencies via composer:
```bash
$ curl -s http://getcomposer.org/installer | php
$ php composer.phar install
```

At the moment, performing unit tests aren't possible. In the future, you'll be able to do them.
For now, thank you. Feel free to contribute with anything you think you can.
