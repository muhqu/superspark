

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

basic usage
-----------

Read values via script arguments.
```bash
$ superspark 1 2 3 5 8 15 26



  ̄̄ ̄̄̄ ̄̄̄̄ ̄̄̄̄̄ ̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄
```

Read values from *stdin*. One value per line.
```bash
$ seq 0 18 | superspark



  ̄ ̄̄ ̄̄̄ ̄̄̄̄ ̄̄̄̄̄ ̄̄̄̄̄̄ ̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄
```


advanced usage
--------------

Repeatedly exec `CMD` to read values. One value per line. Sleep `N` seconds between redraws.
```bash
$ superspark -n 1 -c "seq 0 40 | awk '{
    printf \"%6d\\n\", (sin((systime()+\$1)/2)*cos((systime()+\$1)/4)+1)*20;
  }'"



  ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄ ̄̄̄̄ ̄̄̄̄ ̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄ ̄̄̄̄̄ ̄̄̄̄ ̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄ ̄̄̄̄ ̄̄̄̄ ̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄ ̄̄̄̄ ̄̄̄̄̄ ̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄
```


Continuously read from *stdin* and draw an accumulated graph with every new value. One value per line.
```bash
$ ping -n localhost | awk 'BEGIN{FS="time=|ms"}{
    printf "%d\n", $2*1000;fflush();}' | superspark -s -L



  ̄ ̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄ ̄̄̄̄̄̄̄̄̄̄̄̄̄̄̄
 min: 0      max: 126    curr: 93     mean: 98.79
```


how does it work?
-----------------

The sparklines are assembled using the unicode [combining character][] `U+0304` which is named *COMBINING MACRON*. ...like an apostrophe dash. So, this obviously only works on full-fledged UTF-8 enabled terminals... e.g. [iTerm 2][], Terminal.app on Mac. Don't know about windows/linux support yet...


who?
----

|   |   |
|---|---|
| ![](http://gravatar.com/avatar/0ad964bc2b83e0977d8f70816eda1c70) | © 2013 by Mathias Leppich <br>  [github.com/muhqu](https://github.com/muhqu), [@muhqu](http://twitter.com/muhqu) |
|   |   |


[source]: https://github.com/muhqu/superspark/blob/master/superspark
[php]: http://www.php.net
[Zach Holman]: https://github.com/holman
[spark]: https://github.com/holman/spark
[combining character]: http://en.wikipedia.org/wiki/Combining_character
[iTerm 2]: http://www.iterm2.com/
