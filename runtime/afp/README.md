# Configuration for searching mounted file systems

This configuration for Nutch is setup to search a mounted AFP volume.  Currently, the `conf/regex-urlfilter.txt` file
has to contain the name of the directory that was mounted.  This is to ensure that the crawler does not escape from the
mounted directory.  You will need to update this for your checkout.  There is a setting in Nutch that removes the
need for this, but it has not been turned on and tested yet.
