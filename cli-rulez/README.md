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

