Powershell stuff
================

Output streams
--------------

There are 6 output streams (success, error, warning, verbose, debug, information).

Example:

```
&{
   Write-Warning "a warning"
   Write-Error   "an error"
   Write-Verbose "verbose text"
} 4> C:\temp\verbose.log
```

See [official documentation](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_redirection?view=powershell-7.2).


Redirect output
---------------

Write all streams to a log file.

`some-command *> c:\temp\output.log`


Generate matrix list
--------------------

A matrix for
- 1, 2, 3, 17
- a, b

`1..3+17 | % { ("server-a-{0:d2}" -f $_), ("server-b-{0:d2}" -f $_) }`

Results in:

```
server-a-01
server-b-01
server-a-02
server-b-02
server-a-03
server-b-03
server-a-17
server-b-17
```

The inner part can also be rewritten as loop:

`1..3+17 | % { $nr = $_ ; "a","b" | % { "server-{0}-{1:d2}" -f $_,$nr } }`
