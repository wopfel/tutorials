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


comm
----

Compare two text files and shows lines only in file1 (1st column), only in file2 (2nd column), and lines in both files (3rd column).

Example: `comm file1.txt file2.txt`

Find common lines in both files: `comm -12 <(sort file1.txt) <(sort file2.txt)`


cdrecord
--------

Write an ISO image to a CD.

Example: `cdrecord dev=/dev/sr1 speed=12 -dao -eject -v Downloads/clonezilla-live-2.6.4-10-amd64.iso`


ts
--

Timestamp each line. Very useful in a pipe. Package moreutils on Arch Linux. @climagic on Twitter added a `stdbuf -o0 uniq |` before the ts command to only show the line when it has changed (different to previous output line from ps).

Example: `while ps auxw | grep '[d]dclient' ; do sleep 5 ; done | ts`

Example output:

```
Jan 24 16:23:44 root         336  0.0  3.6  21684 13632 ?        S    14:33   0:00 ddclient - sleeping for 20 seconds
Jan 24 16:23:49 root         336  0.0  3.6  21684 13632 ?        S    14:33   0:00 ddclient - sleeping for 10 seconds
Jan 24 16:23:54 root         336  0.0  3.6  21684 13632 ?        S    14:33   0:00 ddclient - sleeping for 10 seconds
Jan 24 16:23:59 root         336  0.0  3.6  21684 13632 ?        S    14:33   0:00 ddclient - sleeping for 300 seconds
Jan 24 16:24:04 root         336  0.0  3.6  21684 13632 ?        S    14:33   0:00 ddclient - sleeping for 300 seconds
Jan 24 16:24:09 root         336  0.0  3.6  21684 13632 ?        S    14:33   0:00 ddclient - sleeping for 290 seconds
```


progress
--------

Shows the progress of different commands. Can be started when dd is already running. Detects dd, rsync, and many other programs.

Example output of `progess --monitor`:

```
[ 2013] dd /dev/dm-13
        8.5% (5.1 GiB / 60 GiB) 8.0 MiB/s remaining 1:57:12

[ 2017] dd /dev/dm-12
        96.6% (4.8 GiB / 5 GiB) 8.0 MiB/s remaining 0:00:21
```

