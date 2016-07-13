# krabkopy
Batch remote copy utility script.

## How to get help ?

kopy --help

(Why is it not "-h" like everyone else ? -- because -h is for setting up a host)


## Is there any prerequisite ?

Yes :
 - Perl 5.18.02+
 - JSON::XS
 - Net::SCP
 - a corectly set up SSH host that uses a RSA key (no password will ever be asked to you)


## How do I install that ?

Clone the repo (or donwload the file) into some location you know (either directly in a bin directory, but... meh; or in a directory that is in your PATH; or in a random directory and then ln -s).
Chmod it to make it executable.
You can now run the script with "kopy" !

Note: when running kopy , if you get an error like "kopy: /usr/bin/perl: bad interpreter: No such file or directory",
it means that the Perl executable is not in /usr/bin/perl.
You should maybe create a symbolic link (ln -s /path/to/perl /usr/bin/perl, "/path/to/perl" being the actual path of your perl executable), move perl (not recommended) or change the kopy file (if you feel adventurous).

Changing the kopy file : 
1. Open "kopy" with a text editor
2. Find a line that looks like '#!/usr/bin/perl'
3. Change it to '#!/path/to/perl' where /path/to/perl is the actual path to the perl binary.
4. Save and quit.
5. Here you go.


## How do I use it ?

1. Go to a directory where there are files you want to upload to a remote location.
2. Set up SSH/SCP options by running kopy with various options (host with -h, user with -u, destination directory with -d)
3. Add files by running kopy with -f and -fr or remove them by using -r
4. You can review your options and your files by running kopy with -p
5. Send your files by running kopy with -s
6. If you don't want to use kopy ever again in this directory, you can run kopy -c. Note that you will still have a configuration file in this directory, but containing an empty JSON (that is : {})

kopy is a little bit smart on what it sends : if it detects that it already sent a file that has not been modified since the last copy, it will not send it again. This behaviour can be bypassed by using -sr isntead of -s.

When using -f, you can specify files, directories and wildcarded pathes. When using directories, you can use -fr instead of -f to recursively add directories. (Specifying -fr when using wildcards is useless; it will only check for files in the current directory, and will not go further).


## Example ?

  kopy -u krab -h krabtlantid
  kopy -d "~/destination/"
  kopy -fr ./tests/ -f Makefile script.pl *.cpp headers/*.h
  kopy -p
  kopy -s


## How does it work ?

I would say that my code is "self-explanatory" but... meh; not that much actually.
Long story short, the program stores configuration in a hidden file (.copyproject) in the directory you ran kopy in the form of a JSON.
Of course, you should NEVER modify this file by yourself, unless you know what you do.


## Is there [insert here a feature there is not] ?

No.


## Will there be ?

Erf... I cannot promise anything. If the feature is interesting and/or cool (and not too hard to implement) I don't see why not; but I cannot guarantee I will have the time to do that.
