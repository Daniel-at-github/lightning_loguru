## \

![](./figures/logo.svg){width=90%}

Slides: [https://daniel-at-github.github.io/lightning_loguru/](https://daniel-at-github.github.io/lightning_loguru/)

## Install

~~~ bash
pipenv shell
pipenv install loguru
~~~

## Usage

~~~ python
from loguru import logger
logger.debug("Hello Python Vigo")
~~~

<style type="text/css">
.ansi2html-content { display: inline; white-space: pre-wrap; word-wrap: break-word; }
.body_foreground { color: #AAAAAA; }
.body_background { background-color: #000000; }
.body_foreground > .bold,.bold > .body_foreground, body.body_foreground > pre > .bold { color: #FFFFFF; font-weight: normal; }
.inv_foreground { color: #000000; }
.inv_background { background-color: #AAAAAA; }
.ansi1 { font-weight: bold; }
.ansi32 { color: #00aa00; }
.ansi34 { color: #0000aa; }
.ansi36 { color: #00aaaa; }
</style>

<pre class="ansi2html-content">
<span class="ansi32">2018-12-20 15:13:28.412</span> | <span class="ansi34"></span><span class="ansi1 ansi34">DEBUG   </span> | <span class="ansi36">__main__</span>:<span class="ansi36">&lt;module&gt;</span>:<span class="ansi36">3</span> - <span class="ansi34"></span><span class="ansi1 ansi34">Hello Python Vigo</span>
</pre>

## Custom formats

You could replace de default sink with a custom format

~~~ python
from loguru import logger
import sys
logger.remove()
logger.add(sys.stderr,
           format="{time} {level} {message}",
           filter=None,
           level="DEBUG")
logger.success("Another example deployed")
~~~

~~~
2018-12-20T15:50:56.536470+0100 SUCCESS Another example deployed
~~~

## Levels

~~~ python
from loguru import logger
import sys
logger.remove()
logger.add(sys.stderr, level="TRACE",
           format='<level>{level: <8}</level> '
                  '=> <level>{message}</level>')
logger.trace("log data")
logger.debug("log data")
logger.info("log data")
logger.success("log data")
logger.warning("log data")
logger.error("log data")
logger.critical("log data")
~~~

<style type="text/css">
.ansi2html-content { display: inline; white-space: pre-wrap; word-wrap: break-word; }
.body_foreground { color: #AAAAAA; }
.body_background { background-color: #000000; }
.body_foreground > .bold,.bold > .body_foreground, body.body_foreground > pre > .bold { color: #FFFFFF; font-weight: normal; }
.inv_foreground { color: #000000; }
.inv_background { background-color: #AAAAAA; }
.ansi1 { font-weight: bold; }
.ansi31 { color: #aa0000; }
.ansi32 { color: #00aa00; }
.ansi33 { color: #aa5500; }
.ansi34 { color: #0000aa; }
.ansi36 { color: #00aaaa; }
.ansi41 { background-color: #aa0000; }
</style>

<pre class="ansi2html-content">
<span class="ansi36"></span><span class="ansi1 ansi36">TRACE   </span> =&gt; <span class="ansi36"></span><span class="ansi1 ansi36">log data</span>
<span class="ansi34"></span><span class="ansi1 ansi34">DEBUG   </span> =&gt; <span class="ansi34"></span><span class="ansi1 ansi34">log data</span>
<span class="ansi1">INFO    </span> =&gt; <span class="ansi1">log data</span>
<span class="ansi32"></span><span class="ansi1 ansi32">SUCCESS </span> =&gt; <span class="ansi32"></span><span class="ansi1 ansi32">log data</span>
<span class="ansi33"></span><span class="ansi1 ansi33">WARNING </span> =&gt; <span class="ansi33"></span><span class="ansi1 ansi33">log data</span>
<span class="ansi31"></span><span class="ansi1 ansi31">ERROR   </span> =&gt; <span class="ansi31"></span><span class="ansi1 ansi31">log data</span>
<span class="ansi41"></span><span class="ansi1 ansi41">CRITICAL</span> =&gt; <span class="ansi41"></span><span class="ansi1 ansi41">log data</span>
</pre>

## File logging

~~~ python
# File timestamp
logger.add("file_{time}.log")
# Rotation by size, once a day or at X days
logger.add("file_1.log", rotation="500 MB")    # too big
logger.add("file_2.log", rotation="12:00")     # at noon
logger.add("file_3.log", rotation="1 week")    # after a week
# Cleanup by time
logger.add("file_X.log", retention="10 days")
# Compress to save space
logger.add("file_Y.log", compression="zip")
~~~

## String formatting using braces

~~~ python
logger.success("If you're using Python {}, better with {feature}",
               3.6,
               feature="f-strings")
~~~

<style type="text/css">
.ansi2html-content { display: inline; white-space: pre-wrap; word-wrap: break-word; }
.body_foreground { color: #AAAAAA; }
.body_background { background-color: #000000; }
.body_foreground > .bold,.bold > .body_foreground, body.body_foreground > pre > .bold { color: #FFFFFF; font-weight: normal; }
.inv_foreground { color: #000000; }
.inv_background { background-color: #AAAAAA; }
.ansi32 { color: #00aa00; }
</style>

<pre class="ansi2html-content">
<span class="ansi32"></span><span class="ansi1 ansi32">SUCCESS </span> =&gt; <span class="ansi32"></span><span class="ansi1 ansi32">If you're using Python 3.6, better f-strings</span>

</pre>

## Asynchronous logs

Asynchronous, Thread-safe, Multiprocess-safe

~~~ python
logger.add("somefile.log", enqueue=True)
~~~


## Exceptions

~~~ python
from loguru import logger

@logger.catch
def my_function(x, y, z):
    # An error? It's catched anyway!
    return 1 / (x + y - z)

my_function(1, 2, 3)
~~~

## Exceptions

<style type="text/css">
.ansi2html-content { display: inline; white-space: pre-wrap; word-wrap: break-word; }
.body_foreground { color: #AAAAAA; }
.body_background { background-color: #000000; }
.body_foreground > .bold,.bold > .body_foreground, body.body_foreground > pre > .bold { color: #FFFFFF; font-weight: normal; }
.inv_foreground { color: #000000; }
.inv_background { background-color: #AAAAAA; }
.ansi1 { font-weight: bold; }
.ansi31 { color: #aa0000; }
.ansi32 { color: #00aa00; }
.ansi33 { color: #aa5500; }
.ansi35 { color: #E850A8; }
.ansi36 { color: #00aaaa; }
.ansi38-15 { color: #ffffff; }
.ansi38-197 { color: #d2002a; }
.ansi38-141 { color: #7e54d2; }
.ansi38-81 { color: #2aa8d2; }
</style>

<pre class="ansi2html-content">
<span class="ansi32">2018-12-20 16:38:37.569</span> | <span class="ansi31"></span><span class="ansi1 ansi31">ERROR   </span> | <span class="ansi36">__main__</span>:<span class="ansi36">&lt;module&gt;</span>:<span class="ansi36">9</span> - <span class="ansi31"></span><span class="ansi1 ansi31">An error has been caught in function '&lt;module&gt;', process 'MainProcess' (8465), thread 'MainThread' (140530453767936):</span>
<span class="ansi33"></span><span class="ansi1 ansi33">Traceback (most recent call last):</span><span class="ansi33"></span>

&gt; File "<span class="ansi32"></span><span class="ansi1 ansi32">example.py</span><span class="ansi32"></span>", line <span class="ansi33">9</span>, in <span class="ansi35">&lt;module&gt;</span>
<span class="ansi38-15">    </span><span class="ansi38-15">my_function</span><span class="ansi38-15">(</span><span class="ansi38-141">1</span><span class="ansi38-15">,</span><span class="ansi38-15"> </span><span class="ansi38-141">2</span><span class="ansi38-15">,</span><span class="ansi38-15"> </span><span class="ansi38-141">3</span><span class="ansi38-15">)</span>
    <span class="ansi36">└ </span><span class="ansi1 ansi36">&lt;function my_function at 0x7fcfc9725268&gt;</span><span class="ansi36"></span>

  File "<span class="ansi32"></span><span class="ansi1 ansi32">example.py</span><span class="ansi32"></span>", line <span class="ansi33">7</span>, in <span class="ansi35">my_function</span>
<span class="ansi38-15">    </span><span class="ansi38-81">return</span><span class="ansi38-15"> </span><span class="ansi38-141">1</span><span class="ansi38-15"> </span><span class="ansi38-197">/</span><span class="ansi38-15"> </span><span class="ansi38-15">(</span><span class="ansi38-15">x</span><span class="ansi38-15"> </span><span class="ansi38-197">+</span><span class="ansi38-15"> </span><span class="ansi38-15">y</span><span class="ansi38-15"> </span><span class="ansi38-197">-</span><span class="ansi38-15"> </span><span class="ansi38-15">z</span><span class="ansi38-15">)</span>
    <span class="ansi36">            │   │   └ </span><span class="ansi1 ansi36">3</span><span class="ansi36"></span>
    <span class="ansi36">            │   └ </span><span class="ansi1 ansi36">2</span><span class="ansi36"></span>
    <span class="ansi36">            └ </span><span class="ansi1 ansi36">1</span><span class="ansi36"></span>

<span class="ansi31"></span><span class="ansi1 ansi31">ZeroDivisionError</span><span class="ansi31"></span>:<span class="ansi1"> division by zero
</span>
</pre>


## Structured logging

~~~ python
from loguru import logger
logger.add("log.json",
           serialize=True,
           level="DEBUG")
logger.success("Mechanized!!")
~~~

~~~ json
{"record": {"message": "Mechanized!!", "line": 5, "name": "__main__", "level": {"icon": "\u2714\ufe0f", "name": "SUCCESS", "no": 25}, "function": "<module>", "file": {"path": "example.py", "name": "example.py"}, "module": "example", "elapsed": {"repr": "0:00:00.001335", "seconds": 0.001335}, "time": {"repr": "2018-12-20 17:49:29.347426+01:00", "timestamp": 1545324569.347426}, "extra": {}, "thread": {"name": "MainThread", "id": 140491034552064}, "exception": null, "process": {"name": "MainProcess", "id": 9793}}, "text": "2018-12-20 17:49:29.347 | SUCCESS  | __main__:<module>:5 - Mechanized!!\n"}
~~~


## Structured logging

~~~ json
{
  "record": {
    "message": "Mechanized!!",
    "line": 5,
    "name": "__main__",
    "level": {
      "icon": "\u2714\ufe0f️",
      "name": "SUCCESS",
      "no": 25
    },
    "function": "<module>",
    "file": {
      "path": "example.py",
      "name": "example.py"
    },
    "module": "example",
    "elapsed": {
      "repr": "0:00:00.001335",
      "seconds": 0.001335
    },
    "time": {
      "repr": "2018-12-20 17:49:29.347426+01:00",
      "timestamp": 1545324569.347426
    },
    "extra": {},
    "thread": {
      "name": "MainThread",
      "id": 140491034552064
    },
    "exception": null,
    "process": {
      "name": "MainProcess",
      "id": 9793
    }
  },
  "text": "2018-12-20 17:49:29.347 | SUCCESS  | __main__:<module>:5 - Mechanized!!\n"
}
~~~

## and much more

* Lazy evaluation of expensive functions
* Customizable levels
* Better datetime handling
* Suitable for scripts and libraries
* Entirely compatible with standard logging
* Personalizable defaults through environment variables
* Convenient parser
* Exhaustive notifier

## Credits

**Python packages**\
[**loguru**](https://pypi.org/project/loguru/)\
[**ansi2html**](https://pypi.org/project/ansi2html/) - capturing terminal log colors\
[**markdownreveal**](https://pypi.org/project/markdownreveal/) - slides\

**Github**\
[https://daniel-at-github.github.io/lightning_loguru/](https://daniel-at-github.github.io/lightning_loguru/)
