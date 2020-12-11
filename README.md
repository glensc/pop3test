This is an example to reproduce the following issue:
https://github.com/laminas/laminas-mail/issues/6

To run this example, you need to download this example, 
change into the directory and install (tested on Ubuntu 18.04):

`composer require laminas/laminas-mail`

Then start the test mail server using (it continues to run in the background):

`python3 start_flyingrat.py`

The script also sends the example email test.eml to the mail server.

The PHP script testpop3.php then will try to fetch the email:

`php testpop3.php`

And fail with this exception:
```
Number of messages: 1
PHP Fatal error:  Uncaught Laminas\Mail\Exception\RuntimeException: Line "--===============1019615746237534981==" does not match header format! in /home/vagrant/pop3test/vendor/laminas/laminas-mail/src/Headers.php:119
Stack trace:
#0 /home/vagrant/pop3test/vendor/laminas/laminas-mail/src/Storage/Part.php(113): Laminas\Mail\Headers::fromString('Content-Type: m...')
#1 /home/vagrant/pop3test/vendor/laminas/laminas-mail/src/Storage/Message.php(53): Laminas\Mail\Storage\Part->__construct(Array)
#2 /home/vagrant/pop3test/vendor/laminas/laminas-mail/src/Storage/Pop3.php(64): Laminas\Mail\Storage\Message->__construct(Array)
#3 /home/vagrant/pop3test/testpop3.php(21): Laminas\Mail\Storage\Pop3->getMessage(1)
#4 {main}
  thrown in /home/vagrant/pop3test/vendor/laminas/laminas-mail/src/Headers.php on line 119
```
