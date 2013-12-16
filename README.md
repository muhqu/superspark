

Superspark
==========

Inspired by [Zach Holman][]'s [spark][], it brings sparklines, with greater detail, to your shell.

See the demo: 

![](https://raw.github.com/muhqu/superspark/master/demo.gif)


install
-------

`superspark` is a [shell script][source] that wraps arround a tiny [php][] command line script. For it to run you need php 5.3 (or above) and need to place the script somewhere on your `$PATH`.

```bash
wget https://raw.github.com/muhqu/superspark/master/superspark \
  -O /usr/local/bin/superspark
chmod +x /usr/local/bin/superspark
superspark -h
```

how does it work?
-----------------

The sparklines are assembled using the unicode [combining character][] `U+0304` which is named *COMBINING MACRON*. ...like an apostrophe dash. So, this obviously only works on full-fledged UTF-8 enabled terminals... e.g. [iTerm 2][], Terminal.app on Mac. Don't know about windows/linux support yet...


----

[source]: https://github.com/muhqu/superspark/blob/master/superspark
[php]: http://www.php.net
[Zach Holman]: https://github.com/holman
[spark]: https://github.com/holman/spark
[combining character]: http://en.wikipedia.org/wiki/Combining_character
[iTerm 2]: http://www.iterm2.com/
