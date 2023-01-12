# dict-wrapper
Wrapper to combine access to DICT using curl, and spell checking using aspell 

Major purpose is to provide dict functionality via the command mode on cygwin, as dictd is lacking.
But the wrapper can be used on any unix platform with a bash.

Requires 2 packages to be present on the platform
aspell + dictionaries
curl

To use this wrapper just put it somewhere in your path: e.g. /usr/local/bin/
To install the dependencies on cygwin:
- You can do this with the cygwin setup program. Use the dependency packages from below
- But I prefer to use apt-cyg as it doesn't update all your other packages by default.
  - Use any browser to get apt-cyg e.g.:
     lynx -source rawgit.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg
     or 
     wget https://rawgit.com/transcode-open/apt-cyg/master/apt-cyg -O apt-cyg
  - Install apt-cyg into cygwin, apt-cyg is just a bash script, so you can inspect the code if you want to :-)
     install apt-cyg /bin
     hash -r  # to pick up apt-cyg or start a new bash.
  - Now we can install our dependencies  
     apt-cyg install aspell aspell-en 
     apt-cyg install curl
  - For additional dictionaries use
     apt-cyg searchall aspell
    And install the ones you need
- Now the list of dictionaries for aspell is limited on cygwin. But there are many dictionaries
  available on line. As an example we will in stall a dutch aspell directory. As before you can download with any browser
  but here we use lynx.
    $ cd /tmp
    $ lynx -source gnu.mirror.constant.com/aspell/dict # show all available
    $ lynx -source gnu.mirror.constant.com/aspell/dict/nl # show dutch dictionaries
    $ lynx -source gnu.mirror.constant.com/aspell/dict/nl/aspell-nl-0.50-2.tar.bz2 > aspell-nl-0.50-2.tar.bz2 # get it 
    $ 7z x aspell-nl-0.50-2.tar.bz2  # 7z is in cygwin package p7zip
    $ tar -xvf aspell-nl-0.50-2.tar
    $ cd aspell-nl-0.50-2
    $ cat README # to check that methode below is still correct :-) 
    $ ./configure
    $ make # skipped 3 dutch words (no problem):  "rock-'n-roll" "rock-'n-roller" "spring-in-'t-veld"
    $ make install
  Check that the library was added correctly
    $ dict -c -l nl "kaaskop kaskop"
    @(#) International Ispell Version 3.1.20 (but really Aspell 0.60.8)
    *
    & kaskop 11 8: kaaskop, kas kop, kas-kop, kaalkop, keikop, kaaskoper, leeskop, loskoop, luiskop, kesp, kroeskop

You are done

Some examples:
  $ dict -? # show the manual page.
  
  $ dict dragonfly
  150 1 definitions retrieved
  151 "dragonfly" wn "WordNet (r) 3.0 (2006)"
  dragonfly
      n 1: slender-bodied non-stinging insect having iridescent wings
           that are outspread at rest; adults and nymphs feed on
           mosquitoes etc. [syn: {dragonfly}, {darning needle},
           {devil's darning needle}, {sewing needle}, {snake feeder},
           {snake doctor}, {mosquito hawk}, {skeeter hawk}]
  .
  
  $ dict -c "dragonfly dragonflie"
  @(#) International Ispell Version 3.1.20 (but really Aspell 0.60.8)
  * 
  & dragonflie 3 10: dragonflies, dragonfly, dragonfly's
  
  $ dict -c c:/temp/measure_pu.html --mode=html  # spellcheck a html file (see aspell --help) 
