Install
================

FIRST: Set the Initial User !!!!
* Line 5 of buildout.cfg


Buildout
#------------
python bootstrap.py
./bin/buildout -c prod.cfg    # add -vvvvv if you want lots of verbiage

#Start-up Plone
#---------------
./bin/startcluster.sh

install site: merced


install plonetheme.merced



Setup Apache
=======================

My Apache virtualhost looks like this:

<VirtualHost *:80>

    ServerName merced.tool.net

	ServerAdmin webmaster@localhost
	DocumentRoot /web/cameron/merced/merced-buildout/src/merced.xdvtheme/merced/xdvtheme/xdvparts
	<Directory /web/cameron/merced/merced-buildout/src/merced.xdvtheme/merced/xdvtheme/xdvparts>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride None
		Order allow,deny
		allow from all
	</Directory>

	ErrorLog /web/log/merced.error.log
	# Possible values include: debug, info, notice, warn, error, crit,
	# alert, emerg.
	LogLevel warn
	CustomLog /web/log/merced.access.log combined


  <Location />
  Order Allow,deny
  Allow from all
  </Location>

  #Header set X-UA-Compatible "IE=EmulateIE8"

  RewriteEngine On
  RewriteCond %{REQUEST_URI} !^/static/
  RewriteRule ^($|/.*) \
    http://127.0.0.1:20101/VirtualHostBase/http/%{SERVER_NAME}:80/merced/VirtualHostRoot/$1 [P,L]
  #_vh_tool-zope
  #http://127.0.0.1:200101/VirtualHostBase/\
  #http://%{SERVER_NAME}:80/xxxxxx/VirtualHostRoot$1 [L,P]

</VirtualHost>



To Do
==========================
* Front Page
* The caching stuff
  * add squid or Varnish?
* The footer
