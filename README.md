# dict-wrapper
Wrapper to combine access to DICT using curl, and spell checking using aspell 

Major purpose is to provide dict functionality via the command mode on cygwin, as dictd is lacking.
But the wrapper can be used on any unix platform with a bash.

Requires 2 packages to be present on the platform
aspell + dictionaries
curl

To use this wrapper just put it somewhere in your path: e.g. /usr/local/bin/
To install the dependencies:
