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

`1..10 | % { "server-a-{0:d2}" -f $_, "server-b-{0:d2}" -f $_ }`

#TODO: Check if it works that way, add output example
