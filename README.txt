A series of simple lessons in WebGL, plus some related examples.

The folders named lesson01, lesson02, and so on are a sequential tutorial
and are best understood using the explanatory text at:

    <http://learningwebgl.com/>

The form of the lessons is *very* loosely based on NeHe Productions'
well-known OpenGL tutorial, which can be found here:

    <http://nehe.gamedev.net/>


The folders named example01 etc are example code for interesting
stuff outside the scope of the tutorial, and have their own README.txt
files with details.

When experimenting with the lessons in Chrome you will need to run them from an 
local web server to avoid security issues loading from a different origin.

Setup an Apache localhost for webgl-lessons on Mac OS X

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

After making the change in the Apache vhost configuration first confirm the the syntax for the Apache configuration is still correct:

    $ apachectl configtest
    Syntax OK

If the syntax is OK then restart Apache:

    $ sudo apachectl restart

Now you can open the webgl-lessons in any local browser at this url: http://webgl-lessons.local/
