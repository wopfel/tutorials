cli stuff
=========

Every now and then I see a Linux(, ...) cli command I've never seen before. The difficult part is to remember it when I need it.

envsubst
--------

Substitute environment variables in a text file. Seen in the Docker sample about Nginx.


entr
----

Run a command when a file (or more files) changes.

Sample usage: `ls | entr echo bla`


ack
---

Search files like grep, excluding .git (and other VCS dirs) automatically.

Example: `ack --perl needle`


jo
--

Create JSON output by a shell command.

Example: `jo name=Jane`

Prints `{"name":"Jane"}`

There are much more possibilites. See [Jan-Piet Mens' site](https://jpmens.net/2016/03/05/a-shell-command-to-create-json-jo/) for a detailed description.


Icinga
------

```
/usr/local/share/icingaweb2/bin/icingacli monitoring list hosts --problems --verbose
/usr/local/share/icingaweb2/bin/icingacli monitoring list services --problems --verbose
```


dstat
-----

Show statistics about system resources. Similar to vmstat and iostat. Includes network throughput.

![ScreenShot](images/dstat-sample.png)

Category: performance


fio
---

Benchmark testing. Disk throughput.

Example: `fio --rw=readwrite --name=test --size=200M --bs=4M --numjobs=2 --group_reporting --runtime=20 --time_based --refill_buffers`


bc
--

Calculator.

Example: `echo "scale=1000; 4*a(1)" | bc -l`
Calculates 1000 digits for Pi.

