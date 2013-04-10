------------------------------------------------------------------
The official maintained repository for this project is now
https://github.com/tparisi/webgl-lessons -- please fork from 
and send pull requests to there rather than here.
------------------------------------------------------------------


Some lessons in WebGL
---------------------

This repository contains a series of simple lessons in WebGL, plus some
related examples.

The folders named lesson01, lesson02, and so on are a sequential tutorial and
are best understood using the explanatory text at:

    <http://learningwebgl.com/lessons/>

The form of the first ten lessons is *very* loosely based on NeHe Productions'
well-known OpenGL tutorial, which can be found here:

    <http://nehe.gamedev.net/>

The lessons from 11 onwards are not related to the NeHe ones.

The folders named example01 etc are example code for interesting stuff outside
the scope of the tutorial, and have their own README.txt files with details.


Problems seeing the lessons?
----------------------------

When experimenting with the lessons later than #5 you may encounter errors
resulting from "cross-origin" file access.  This is caused by the browsers'
security systems:

 * Browsers want to stop pages from one server ("origin") from gaining access
   to data from another origin except under closely-controlled circumstances.
   (For example, imagine if a hostile website tried to gain access to data
   from the online banking window you had open in another tab.)
 * Unfortunately, when files are loaded from the filesystem, the browser sees
   each file as a separate origin.  So when one of these examples tries to
   load, say, a texture to display on a cube, it will fail.

There are two ways you can work around this.  The best, safest way is to use
a local webserver, but an alternative if you're careful about it is to
temporarily disable the cross-origin restrictions.

The dangerous way
~~~~~~~~~~~~~~~~~

Switch off the same-origin policy.  This is perfectly safe if you're only
going to use the browser for testing your own code, but isn't a good idea
in general (it's all too easy to casually browse over to an internet site
without thinking about it).  Still, if you want to do this:

 * Firefox: set the security.fileuri.strict_origin_policy setting in
   about: config to "false".

 * Chrome: use the the --allow-file-access-from-files and
   --disable-web-security switches command-line options (ideally just the
   first).  If you're using a Mac, Stuart Carnie has written a convenient
   application bundle for this here:
   <http://aussiebloke.blogspot.com/2011/08/local-file-system-development-with.html>


The safe way
~~~~~~~~~~~~

Here are instructions on how to run a local web server to host these
lessons using Apache under Mac OS X; GNU/Linux will be similar.  If you're
on Windows, check out Xampp at <http://www.apachefriends.org/en/xampp.html>


1) Add an entry for webgl-lessons.local in /etc/hosts.

This will need to be done as the root user using your preferred editor:

    $ sudo <editor> /etc/hosts

Add the following line and save the file:

    127.0.0.1       webgl-lessons.local

Tell the operating system to flush and reload the local DNS cache:

    dscacheutil -flushcache

Test to see if http://webgl-lessons.local/ is working:

    $ dscacheutil -q host -a name http://webgl-lessons.local/
    name: http://webgl-lessons.local/
    ip_address: <ip_address>

2) Add an Apache vhost configuration:

This will need to be done as the root user using your preferred editor:

    $ sudo <editor> /private/etc/apache2/extra/httpd-vhosts.conf

Add the following vhost configuration replacing <path-to-webgl-lessons> with
the actual path on your filesystem:

    <VirtualHost webgl-lessons.local:80>
       ServerName webgl-lessons
       DocumentRoot <path-to-webgl-lessons>/
       <Directory <path-to-webgl-lessons>>
         Options +Indexes +FollowSymLinks +MultiViews +Includes
         AllowOverride All
         Order allow,deny
         Allow from all
         DirectoryIndex index.html
      </Directory>
    </VirtualHost>

After making the change in the Apache vhost configuration first confirm the
syntax for the Apache configuration is still correct:

    $ apachectl configtest
    Syntax OK

If the syntax is OK then restart Apache:

    $ sudo apachectl restart

Now you can open the webgl-lessons in any local browser at this url:
<http://webgl-lessons.local/>
