I've detailed this out from the very start of the installation (minus most of the installation options except the ones that I think might matter; I did this because I don't want to potentially run into the issue of someone saying they are missing a dependency because the list I gave was based on stuff I had installed and they had not. Certain "creature comforts" were installed by me to ease the burden of an already, imho, an extremely taxing install. But fear not, that's what this guide is for :)

Couple of other notes:
1) The guide is by no stretch of the imagination refined to exactly JUST the steps you need, afterall I start from the very beginning of the distro's install and start choosing window managers and as such will see LibreOffice packages installed. Obviously that is DEFINITELY not needed for the installing/deploying of Huginn :) This means the dependency list is bigger than it should be. This is an area for refinement.
(sorry... I'm just not dealing with a seriously ugly desktop while I do this :) Maybe I'll clone it again and run through it via a full blown terminal screen quickly for non-gui stuff; the default desktop REALLY IS that gross looking!)

2) The narrative of this guide is very informal. The guide is long enough. Until it gets refined down to a very short-order process I've chosen to keep it light and easy to read. That mentioned, I tried to keep the description of the steps as EXACT as possible so it may over time be tiring to read. This is a delicate balance and again, I'm expecting the community to kind've take up the reigns and help on refining this bear.

Anyhow, without further adieu... Let's begin.


**A(/some) note(s) about option(s) used during installation:**
* Add Online Repositories Before Installation - Checked

In the future there will(/may?) be separate sections for the different window manager choices (____if that section continue to stay____)

## Enlightenment Window Manager
### Install packages to make GDM work so Enlightenment can be used

Install gdm-branding-openSUSE:

open xterm
enter the following:

`sudo zypper install gdm-branding-openSUSE`

type the root password then

_hit enter_

You will see something along the lines of:
> Loading repository data...

> Reading installed packages...

> Resolving package dependencies...


> The following 9 applications are going to be installed:

>   Clocks Color Profile Viewer Documents Files LibreOffice Base LibreOffice Calc LibreOffice Draw LibreOffice Impress LibreOffice Writer 


> The following 379 NEW packages are going to be installed:

>   accountsservice apache-commons-logging argyllcms avahi-autoipd bluez brltty brltty-driver-at-spi2 brltty-driver-brlapi brltty-driver-espeak brltty-driver-speech-dispatcher 
>   brltty-driver-xwindow canberra-gtk-play caribou-common clutter-lang colord color-filesystem dbus-1-python3 dhcp dhcp-client dleyna-connector-dbus dleyna-server dnsmasq 
>   dynamic-wallpaper-branding-openSUSE espeak evolution-data-server evolution-data-server-lang flute fortune gconf2 gconf2-branding-openSUSE gconf-polkit gdm gdm-branding-openSUSE 
>   gdmflexiserver geocode-glib gjs gnome-bluetooth gnome-clocks gnome-color-manager gnome-control-center gnome-control-center-color gnome-control-center-user-faces gnome-documents gnome-menus 
>   gnome-menus-branding-openSUSE gnome-online-miners gnome-pty-helper gnome-session gnome-session-core gnome-session-default-session gnome-settings-daemon gnome-shell 
>   gnome-shell-browser-plugin gnome-shell-search-provider-documents gnome-shell-search-provider-gnome-clocks gnome-shell-search-provider-nautilus gnome-themes-accessibility gnome-user-docs 
>   gnome-version google-carlito-fonts grilo-plugins grilo-plugin-tracker grilo-plugin-youtube gstreamer-plugin-gstclutter gstreamer-plugins-bad gstreamer-plugins-good gtk2-engine-hcengine 
>   gtksourceview-lang gupnp-av icc-profiles icc-profiles-basiccolor-lstarrgb icc-profiles-basiccolor-printing2009-coat2 icc-profiles-lcms-lab icc-profiles-mini icc-profiles-openicc-rgb 
>   icc-profiles-scp-argyll icc-profiles-scp-fogra icc-profiles-scp-yamma javapackages-tools libabw-0_1-1 libaccountsservice0 libass5 libbase libboost_date_time1_54_0 libboost_iostreams1_54_0 
>   libbrlapi0_6 libcamel-1_2-49 libcaribou0 libcdr-0_1-1 libcelt0-2 libcheese7 libcheese-common libcheese-gtk23 libclucene-contribs-lib1 libclucene-core1 libclucene-shared1 libclutter-1_0-0 
>   libclutter-gst-2_0-0 libclutter-gtk-1_0-0 libcmis-0_5-5 libcogl20 libcogl-pango20 libcolord-gtk1 libcolorhug2 libcue1 libdleyna-core-1_0-3 libdmapsharing-3_0-2 libdmx1 libdotconf0 
>   libdvdnav4 libdvdread4 libebackend-1_2-7 libe-book-0_1-1 libebook-1_2-14 libebook-contacts-1_2-0 libecal-1_2-16 libedata-book-1_2-20 libedata-cal-1_2-23 libedataserver-1_2-18 libenca0 
>   libetonyek-0_1-1 libevdocument3-4 libevview3-3 libexempi3 libexiv2-13 libexttextcat libexttextcat-2_0-0 libfbembed2_5 libfonts libformula libfreehand-0_1-1 libgdata19 libgdm1 libgee-0_8-2 
>   libgeocode-glib0 libgfbgraph-0_2-0 libgjs0 libGLEW1_10 libgltf-0_0-0 libGLU1 libgme0 libgmime-2_6-0 libgnome-bluetooth13 libgnome-desktop-3_0-common libgnome-desktop-3-10 libgnomekbd 
>   libgnomesu libgnomesu0 libgom-1_0-0 libgrilo-0_2-1 libgrlnet-0_2-0 libgrlpls-0_2-0 libgsf-1-114 libgsm1 libgssdp-1_0-3 libgstallocators-1_0-0 libgstbadbase-1_0-0 libgstbadvideo-1_0-0 
>   libgstbasecamerabinsrc-1_0-0 libgstcodecparsers-1_0-0 libgstgl-1_0-0 libgstmpegts-1_0-0 libgstphotography-1_0-0 libgstrtp-1_0-0 libgstrtsp-1_0-0 libgstsdp-1_0-0 libgsystem0 
>   libgtksourceview-3_0-1 libgtop-2_0-10 libgupnp-1_0-4 libgupnp-av-1_0-2 libgupnp-dlna-2_0-3 libgupnp-dlna-backend-gstreamer libgusb2 libgweather-3-6 libgweather-data libgxps2 libhyphen0 
>   libibus-1_0-5 libical1 libinput5 libiptcdata libiptcdata0 libixion-0_8-0 libjack0 libjavascriptcoregtk-4_0-18 liblangtag1 liblayout libloader liblouis2 liblpsolve55-0 liblrdf2 
>   libmbim-glib0 libmediaart-1_0-0 libmm-glib0 libmms0 libmozjs-24 libmspub-0_1-1 libmusicbrainz5-0 libmutter0 libmwaw-0_3-3 libmythes-1_2-0 libnautilus-extension1 libndp0 libneon27 
>   libnewt0_52 libnm-glib4 libnm-glib-vpn1 libnm-gtk0 libnm-util2 liboauth0 libodfgen-0_1-1 libofa0 libopenal1 libopus0 liborcus-0_8-0 libosinfo libosinfo-1_0-0 libpagemaker-0_0-0 
>   libportaudio2 libproxy1-config-gnome3 libproxy1-networkmanager libpulse-mainloop-glib0 libqmi-glib1 libqmi-tools libquvi libquvi-scripts libraptor2-0 librasqal3 librdf0 libreoffice 
>   libreoffice-base libreoffice-branding-upstream libreoffice-calc libreoffice-draw libreoffice-filters-optional libreoffice-icon-theme-breeze libreoffice-icon-theme-galaxy 
>   libreoffice-icon-theme-hicontrast libreoffice-icon-theme-sifr libreoffice-icon-theme-tango libreoffice-impress libreoffice-l10n-en libreoffice-mailmerge libreoffice-math libreoffice-pyuno 
>   libreoffice-share-linker libreoffice-templates-en libreoffice-templates-labels-a4 libreoffice-templates-labels-letter libreoffice-templates-presentation-layouts libreoffice-writer 
>   librepository librevenge-0_0-0 libserializer libslang2 libSoundTouch0 libspandsp2 libspeechd2 libstartup-notification-1-0 libtag1 libtag_c0 libtelepathy-logger3 libtotem-plparser18 
>   libtracker-common-1_0 libtracker-control-1_0-0 libtracker-miner-1_0-0 libtracker-sparql-1_0-0 libvdpau1 libvisio-0_1-1 libvte-2_91-0 libwacom2 libwacom-data libwavpack1 libwayland-egl1 
>   libwebkit2gtk3-lang libwebkit2gtk-4_0-37 libwnck-3-0 libwpd-0_10-10 libwpg-0_3-3 libwps-0_4-4 libxcb-xf86dri0 libxklavier16 libXRes1 libxslt-tools libzapojit-0_0-0 lua luasocket 
>   Mesa-demo-x mobile-broadband-provider-info ModemManager mutter mutter-data myspell-dictionaries myspell-en myspell-lightproof-en nautilus nautilus-extension-tracker-tags NetworkManager 
>   NetworkManager-gnome openal-soft orca pentaho-libxml pentaho-reporting-flow-engine polkit-gnome python3 python3-atspi python3-brlapi python3-gobject python3-gobject-cairo python3-louis 
>   python3-pip python3-setuptools python3-speechd rp-pppoe sac sbc shared-color-profiles speech-dispatcher speech-dispatcher-module-espeak sushi tcl totem-pl-parser tracker 
>   tracker-miner-files typelib-1_0-AccountsService-1_0 typelib-1_0-Atspi-2_0 typelib-1_0-Caribou-1_0 typelib-1_0-Clutter-1_0 typelib-1_0-ClutterGst-2_0 typelib-1_0-Cogl-1_0 
>   typelib-1_0-CoglPango-1_0 typelib-1_0-EvinceDocument-3_0 typelib-1_0-EvinceView-3_0 typelib-1_0-Gck-1 typelib-1_0-Gcr-3 typelib-1_0-GData-0_0 typelib-1_0-Gdm-1_0 typelib-1_0-GjsPrivate-1_0 
>   typelib-1_0-GnomeBluetooth-1_0 typelib-1_0-GnomeDesktop-3_0 typelib-1_0-Goa-1_0 typelib-1_0-Gst-1_0 typelib-1_0-GstAudio-1_0 typelib-1_0-GstPbutils-1_0 typelib-1_0-GstTag-1_0 
>   typelib-1_0-GstVideo-1_0 typelib-1_0-GSystem-1_0 typelib-1_0-GtkClutter-1_0 typelib-1_0-GtkSource-3_0 typelib-1_0-IBus-1_0 typelib-1_0-JavaScriptCore-3_0 typelib-1_0-JavaScriptCore-4_0 
>   typelib-1_0-Json-1_0 typelib-1_0-Meta-3_0 typelib-1_0-NetworkManager-1_0 typelib-1_0-NMClient-1_0 typelib-1_0-NMGtk-1_0 typelib-1_0-Rest-0_7 typelib-1_0-Soup-2_4 
>   typelib-1_0-TelepathyGlib-0_12 typelib-1_0-TelepathyLogger-0_2 typelib-1_0-Tracker-1_0 typelib-1_0-TrackerControl-1_0 typelib-1_0-UpowerGlib-1_0 typelib-1_0-WebKit2-4_0 
>   typelib-1_0-WebKit-3_0 typelib-1_0-Wnck-3_0 typelib-1_0-Xkl-1_0 typelib-1_0-Zpj-0_0 unoconv usb_modeswitch usb_modeswitch-data webkit2gtk-4_0-injected-bundles xbrlapi xerces-j2-xml-apis 
>   xorg-x11-server-extra zenity zip 


> The following 34 recommended packages were automatically selected:

>   avahi-autoipd brltty clutter-lang dleyna-server dnsmasq espeak evolution-data-server-lang fortune gdm gnome-clocks gnome-control-center gnome-control-center-user-faces gnome-online-miners 
>   gnome-shell-browser-plugin gnome-shell-search-provider-documents grilo-plugins libqmi-tools libwebkit2gtk3-lang ModemManager myspell-lightproof-en nautilus NetworkManager 
>   NetworkManager-gnome openal-soft orca python3-pip rp-pppoe sbc speech-dispatcher tracker tracker-miner-files unoconv usb_modeswitch webkit2gtk-4_0-injected-bundles 


> 379 new packages to install.

> Overall download size: 127.6 MiB. Already cached: 80.4 MiB  After the operation, additional 703.2 MiB will be used.
> Continue? [y/n/? shows all options] (y):

_hit enter_

_log out_

_log back in_

### Fix the desktop environment
You won't have a task bar or "start menu" style of interface yet, DON'T panic!


_Go to the upper right of the screen and click on the tiny down arrow in the menu bar_


You'll know you're looking at the right sub-menu when you see your username listed with a couple of volume sliders at the top. In this menu,

_click the screwdriver/wrench icon in the bottom left of that window_

This will bring up the "All Settings" window.


_Locate the row that is titled: "System"_


_Click the icon that says YaST_


This will pop open a authentication box

_type in the root password_

_hit enter or click continue_


You should now be looking at a window titled: "YaST Control Center @ " and then the hostname of your machine


On the left side of this window is a list of categories for quick display of the appropriate settings on the right side


pane of the window. From this left side,


_click the icon labeled "System"_


The right pane of the window should now show a list of options under the "System" heading.


_Click the icon titled: "/etc/sysconfig" Editor_


This will bring up another window titled: "YaST2 - /etc/sysconfig Editor".


On the left side options


_click the arrow to the left side of the Desktop list item_


multiple options under that should show up


_Locate the sub-option titled: "Display manager"_

_click the arrow next to that option_

_Select the option titled: "DISPLAYMANAGER" from the newly displayed options_


On the right side of the "YaST2 - /etc/sysconfig Editor" window,

_locate the section now showing as: "Setting of: DISPLAYMANAGER"_


There is a drop-down selection box under that text. On the right side of the selection box is a tiny down-arrow.

_Click it_

_select the option labeled: "gdm"_


At the bottom of this window is a button titled: "OK";

_click that_

This will pop up another window titled "YaST2" with a heading titled: "Save Modified Variables",
(if you have more than DISPLAYMANAGER listed than you accidentally made additional selection elsewhere. If this is the case, click cancel, and click the cancel btuton again at the bottom of the "YaST2 - /etc/sysconfig Editor" window. It will then display a pop-up box titled: "YaST2" with the text: "Really abort? All changes will be lost!" click the Yes button. Try re-performing the setting change starting from step # again and work slowly.)


If only DISPLAYMANAGER is listed, then proceed by


_clicking the Save button_


Next,


_click the x button_ (located in the top) for the window titled: "YaST Control Center @ " <and your machine's hostname> right of that window.


_click the x button_ (located in the top right) in the "All Settings" window.


_Click that down arrow_ in the top-right of your desktop to display the window from earlier that had the volume controls and the profile name. There is a button in this window that has the universal symbol for powering a computer on.


_Click this button_


_click the "Restart" button_


Once the system comes back up,


_click your username_


Next to the "Sign In" button is a gear icon.


_Click the gear icon_


_Select the option titled: "Enlightenment"_ from the pop-up box


_Ensure the text cursor is inside of the password text box and enter your password and hit enter or click the "Sign In" button_


Note: if you enter your password incorrectly, there is a good chance your window manager selection will default back to Gnome. If this happens, reclick the gear, and then click the "Enlightenment" option again, enter your password, and then hit enter again or click the "Sign In" button.


### Configure your Enlightenment profile


_Select your keyboard layout_


_click the "Next" button_


In the next window,


_click the selection titled "openSUSE Classic Desktop"_

and then

_click the "Next" button_


In the next window,


_select your window sizing preference_


and then


_click the "Next" button_


Next ensure "Click" is selected in the window titled: "Focus by"


_click the "Next" button_


_Select the graphical checkboxes_ according to your system specifications/preferences 


_click the "Next" button_


Next,


ensure the "Enable Taskbar" option is checked


_click the "Next" button_


Yay! Elegant desktop environment. Ok now that we're FINALLY on the same page...


Next to the chameleon icon in your taskbar is a picture of what resembles a computer screen


_click that_

(If you aren't sure, if you pause the cursor of the picture, it should show a tooltip that says "Terminology".)



# Now onto the actual show:


In the newly created terminal screen enter:

_sudo zypper install git_

(if prompted, type in your root password and hit enter)


_hit enter_


you should see something similiar to:


> Loading repository data...

> Reading installed packages...

> Resolving package dependencies...


> The following 21 NEW packages are going to be installed:

>   cvs cvsps git git-core git-cvs git-email git-gui gitk git-svn git-web libapr1 libapr-util1 libserf-1-1 perl-Authen-SASL perl-Error perl-Net-SMTP-SSL subversion subversion-bash-completion subversion-perl tk 
>   xhost 


> The following 9 recommended packages were automatically selected:

>   git-cvs git-email git-gui gitk git-svn git-web perl-Authen-SASL perl-Net-SMTP-SSL subversion-bash-completion 


> The following package is suggested, but will not be installed:

>   git-daemon 


> 21 new packages to install.

> Overall download size: 9.6 MiB. Already cached: 0 B  After the operation, additional 36.9 MiB will be used.

> Continue? [y/n/? shows all options] (y): 


(packages may differ a little. I already had Firefox installed prior to this)


_hit enter a second time at this prompt_



##Install browser


(if you aren't using the command line completely; some cli (Command-Line Interface) web browser options are: lynx, ELinks, and w3m)


(Note: this is not needed for cloning the huginn GitHub repo, it -may- be needed for downloading Ruby and RVM though; perhaps wget could be used?)


(this tutorial is assuming Firefox usage)


So in the newly created terminal screen enter:


`sudo zypper install firefox`

(if prompted, type in your root password and hit enter)


_hit enter_


(I already had Firefox installed prior to this so I unfortunately, don't have what packages would be needed at this point -- if any beyond just firefox)


_hit enter again_ to confirm


Let's also install a copy of Leafpad for editing files


at the terminal enter:


`sudo zypper install leadpad`

(if prompted, type in your root password and hit enter)


_hit enter_


_hit enter again_ to confirm



##Clone the repository

Enter the following


> cd ~/


_hit enter_


> git clone git://github.com/cantino/huginn.git


_hit enter_


> cd ..


_hit enter_


You should be back at /home/<your username> - (or another way of writing it: ~/)



##Installing MySQL (MariaDB)


Before entering proceeding further, be ready to answer questions about the MySQL database install that is required
questions such as:


* What you want your database root account's password to be


Now enter the following:


> sudo zypper install mysql

(if prompted, type in your root password and hit enter)

_hit enter_


You should now see something along the lines of:

`Retrieving repository 'openSUSE-13.2-Update' metadata `
`..........................................................................................................................`
`...................................[done]`

`Building repository 'openSUSE-13.2-Update' cache `
`..........................................................................................................................`
`........................................[done]`

`Loading repository data...`

`Reading installed packages...`

`'mysql' not found in package names. Trying capabilities.`

`Resolving package dependencies...`

	
`The following 9 NEW packages are going to be installed:`

`libjemalloc1 libmysqlclient18 libmysqlclient_r18 libmysqlcppconn6 libreadline5 libreoffice-base-drivers-mysql mariadb mariadb-client mariadb-errormessages `


`9 new packages to install.`

`Overall download size: 11.2 MiB. Already cached: 0 B  After the operation, additional 107.0 MiB will be used.`

`Continue? [y/n/? shows all options] (y):`


_hit enter_


You may eventually see something like this:


`Retrieving package libjemalloc1-3.6.0-2.1.2.x86_64                                 (1/9), 105.4 KiB (266.8 KiB unpacked)`

`Retrieving: libjemalloc1-3.6.0-2.1.2.x86_64.rpm ...................................................................................................................................................................[done]`

`Retrieving package libmysqlcppconn6-1.1.2-6.2.2.x86_64                             (2/9), 165.0 KiB (668.6 KiB unpacked)`

`Retrieving: libmysqlcppconn6-1.1.2-6.2.2.x86_64.rpm ...............................................................................................................................................................[done]`

`Retrieving package libreadline5-5.2-133.1.2.x86_64                                 (3/9),  96.6 KiB (295.8 KiB unpacked)`

`Retrieving: libreadline5-5.2-133.1.2.x86_64.rpm ...................................................................................................................................................................[done]`

`Retrieving package libmysqlclient18-10.0.25-2.24.1.x86_64                          (4/9), 557.1 KiB (  3.3 MiB unpacked)`

`Retrieving: libmysqlclient18-10.0.25-2.24.1.x86_64.rpm ............................................................................................................................................................[done]`

`Retrieving package mariadb-errormessages-10.0.25-2.24.1.x86_64                     (5/9), 184.5 KiB (  1.9 MiB unpacked)`

`Retrieving: mariadb-errormessages-10.0.25-2.24.1.x86_64.rpm .......................................................................................................................................................[done]`

`Retrieving package libmysqlclient_r18-10.0.25-2.24.1.x86_64                        (6/9),  31.7 KiB (    0 B unpacked)`

`Retrieving: libmysqlclient_r18-10.0.25-2.24.1.x86_64.rpm ..........................................................................................................................................................[done]`

`Retrieving package mariadb-client-10.0.25-2.24.1.x86_64                            (7/9), 874.2 KiB ( 19.9 MiB unpacked)`

`Retrieving: mariadb-client-10.0.25-2.24.1.x86_64.rpm ..............................................................................................................................................................[done]`

`Retrieving package libreoffice-base-drivers-mysql-5.0.6.3-31.3.x86_64              (8/9), 388.5 KiB (857.5 KiB unpacked)`

`Retrieving: libreoffice-base-drivers-mysql-5.0.6.3-31.3.x86_64.rpm ................................................................................................................................................[done]`

`Retrieving package mariadb-10.0.25-2.24.1.x86_64                                   (9/9),   8.8 MiB ( 79.8 MiB unpacked)`

`Retrieving: mariadb-10.0.25-2.24.1.x86_64.rpm .........................................................................................................................................................[done (2.3 MiB/s)]`

`Checking for file conflicts: ......................................................................................................................................................................................[done]`

`(1/9) Installing: libjemalloc1-3.6.0-2.1.2 ........................................................................................................................................................................[done]`

`(2/9) Installing: libmysqlcppconn6-1.1.2-6.2.2 ....................................................................................................................................................................[done]`

`(3/9) Installing: libreadline5-5.2-133.1.2 ........................................................................................................................................................................[done]`

`(4/9) Installing: libmysqlclient18-10.0.25-2.24.1 .................................................................................................................................................................[done]`

`(5/9) Installing: mariadb-errormessages-10.0.25-2.24.1 ............................................................................................................................................................[done]`

`(6/9) Installing: libmysqlclient_r18-10.0.25-2.24.1 ...............................................................................................................................................................[done]`

`(7/9) Installing: mariadb-client-10.0.25-2.24.1 ...................................................................................................................................................................[done]`

`Additional rpm output:`

`usermod: no changes`


`(8/9) Installing: libreoffice-base-drivers-mysql-5.0.6.3-31.3 .....................................................................................................................................................[done]`

`(9/9) Installing: mariadb-10.0.25-2.24.1 ..........................................................................................................................................................................[done]`

`Additional rpm output:`

`usermod: no changes`


`Update notifications were received from the following packages:`

`mariadb-10.0.25-2.24.1.x86_64 (/var/adm/update-messages/mariadb-10.0.25-2.24.1)`

`View the notifications now? [y/n] (n):`


You can type the letter y and <hit enter> if you like. If you do, you'll likely see something like this:
(Use arrows or pgUp/pgDown keys to scroll the text by lines or pages.)
	
`Message from package mariadb:`
	
	
`You just installed MySQL server for the first time.`

	
`You can start it using:`

`rcmysql start`

	
`During first start empty database will be created for your automatically.`

	
`PLEASE REMEMBER TO SET A PASSWORD FOR THE MariaDB root USER !`

`To do so, start the server, then issue the following commands:`

	
`'/usr/bin/mysqladmin' -u root password 'new-password'`

`'/usr/bin/mysqladmin' -u root -h <hostname> password 'new-password'`

	
`Alternatively you can run:`

`'/usr/bin/mysql_secure_installation'`

	
`which will also give you the option of removing the test`

`databases and anonymous user created by default. This is`

`strongly recommended for production servers.`

	
	
`-----------------------------------------------------------------------------`


###Start the newly installed MySQL (MariaDB) service


`sudo service mysql start`


_hit enter_


(if prompted, type in your root password and hit enter)


Now enter:
/usr/bin/mysql_secure_installation
<hit enter>
You'll see something like this:

	NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
	      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!
	
	In order to log into MariaDB to secure it, we'll need the current
	password for the root user.  If you've just installed MariaDB, and
	you haven't set the root password yet, the password will be blank,
	so you should just press enter here.
	
	Enter current password for root (enter for none):
<hit enter>
You'll see:
	OK, successfully used password, moving on...
	
	Setting the root password ensures that nobody can log into the MariaDB
	root user without the proper authorisation.
	
	Set root password? [Y/n]
Type the letter y and <hit enter>
enter your new database's root password (Make sure it's a GOOD password! Uppercase, Lowercase, Numbers, Symbols, and try for something like 12 characters, longer is better! One note: DO NOT use a $ symbol for the password, it will through the bundle exec rake db:create task off much much later on in the process!!!!)
when you've typed in the password you've choosen <hit enter>
reenter that password again
<hit enter>
You'll now see:
Password updated successfully!
Reloading privilege tables..
 ... Success!