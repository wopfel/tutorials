Setting up TravelStatus-DE-IRIS
-------------------------------

These are the steps how I installed db-iris from https://github.com/derf/Travel-Status-DE-IRIS by @derf.

My environment:
- Ubuntu 19.04 inside LXC container running on Proxmox VE

Installing required packages:

```
apt install git
apt install libmodule-build-perl
apt install libclass-accessor-class-perl libdatetime-perl libdatetime-format-strptime-perl
apt install libgeo-distance-perl liblist-compare-perl liblist-utilsby-perl libtest-compile-perl
apt install liblwp-protocol-https-perl libtext-levenshteinxs-perl libxml-libxml-perl libtext-csv-perl libtest-pod-perl libtest-number-delta-perl libtest-fatal-perl
```

Build db-iris (steps from @derf's Github page):

```
perl Build.PL
./Build
./Build manifest
./Build install
```

Try db-iris:

```
db-iris -od,q 'Dortmund Hbf'
db-iris -od,q 'Nuernberg Hbf'
```

