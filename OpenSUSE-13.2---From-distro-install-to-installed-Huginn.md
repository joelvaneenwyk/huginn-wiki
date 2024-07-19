I've detailed this out from the very start of the installation (minus most of the installation options -- except the ones that I think might matter); I did this because I don't want to potentially run into the issue of someone saying they are missing a dependency because the list I gave was based on stuff I had installed and they had not. Certain "creature comforts" were installed by me to ease the burden of an already, imho, an extremely taxing install. But fear not, that's what this guide is for :)

A few notes:

1. The guide is by no stretch of the imagination refined to exactly JUST the steps you need, afterall I start from the very beginning of the distro's install and start choosing window managers and as such will see LibreOffice packages installed. Obviously that is DEFINITELY not needed for the installing/deploying of Huginn :) This means the dependency list is bigger than it should be. This is an area for refinement.
   (sorry... I'm just not dealing with a seriously ugly desktop while I do this :) Maybe I'll clone it again and run through it via a full blown terminal screen quickly for non-gui stuff; the default desktop REALLY IS that gross looking!)

2. The narrative of this guide is very informal. The guide is long enough. Until it gets refined down to a very short-order process I've chosen to keep it light and easy to read. That mentioned, I tried to keep the description of the steps as EXACT as possible since it may over time be tiring to read. This is a delicate balance and again, I'm expecting the community to kind've take up the reigns and help on refining this bear.

3. There are areas where the steps in this guide can be locked down tighter. One (at least) area to look into is the using of the root password when installing MySQL (MariaDB). While the root password would be needed for system file access (setting up init scripts, installing libraries, etc.), running it as root -- not only seems like a terrible idea -- may not be necessary especially since MySQL is outside of the "well-known" port range.

Anyhow, without further adieu... Let's begin.

**A(/some) note(s) about option(s) used during installation:**

- Add Online Repositories Before Installation - Checked

In the future there will(/may?) be separate sections for the different window manager choices (if that section continue to stay)

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

> Clocks Color Profile Viewer Documents Files LibreOffice Base LibreOffice Calc LibreOffice Draw LibreOffice Impress LibreOffice Writer

> The following 379 NEW packages are going to be installed:

> accountsservice apache-commons-logging argyllcms avahi-autoipd bluez brltty brltty-driver-at-spi2 brltty-driver-brlapi brltty-driver-espeak brltty-driver-speech-dispatcher
> brltty-driver-xwindow canberra-gtk-play caribou-common clutter-lang colord color-filesystem dbus-1-python3 dhcp dhcp-client dleyna-connector-dbus dleyna-server dnsmasq
> dynamic-wallpaper-branding-openSUSE espeak evolution-data-server evolution-data-server-lang flute fortune gconf2 gconf2-branding-openSUSE gconf-polkit gdm gdm-branding-openSUSE
> gdmflexiserver geocode-glib gjs gnome-bluetooth gnome-clocks gnome-color-manager gnome-control-center gnome-control-center-color gnome-control-center-user-faces gnome-documents gnome-menus
> gnome-menus-branding-openSUSE gnome-online-miners gnome-pty-helper gnome-session gnome-session-core gnome-session-default-session gnome-settings-daemon gnome-shell
> gnome-shell-browser-plugin gnome-shell-search-provider-documents gnome-shell-search-provider-gnome-clocks gnome-shell-search-provider-nautilus gnome-themes-accessibility gnome-user-docs
> gnome-version google-carlito-fonts grilo-plugins grilo-plugin-tracker grilo-plugin-youtube gstreamer-plugin-gstclutter gstreamer-plugins-bad gstreamer-plugins-good gtk2-engine-hcengine
> gtksourceview-lang gupnp-av icc-profiles icc-profiles-basiccolor-lstarrgb icc-profiles-basiccolor-printing2009-coat2 icc-profiles-lcms-lab icc-profiles-mini icc-profiles-openicc-rgb
> icc-profiles-scp-argyll icc-profiles-scp-fogra icc-profiles-scp-yamma javapackages-tools libabw-0_1-1 libaccountsservice0 libass5 libbase libboost_date_time1_54_0 libboost_iostreams1_54_0
> libbrlapi0_6 libcamel-1_2-49 libcaribou0 libcdr-0_1-1 libcelt0-2 libcheese7 libcheese-common libcheese-gtk23 libclucene-contribs-lib1 libclucene-core1 libclucene-shared1 libclutter-1_0-0
> libclutter-gst-2_0-0 libclutter-gtk-1_0-0 libcmis-0_5-5 libcogl20 libcogl-pango20 libcolord-gtk1 libcolorhug2 libcue1 libdleyna-core-1_0-3 libdmapsharing-3_0-2 libdmx1 libdotconf0
> libdvdnav4 libdvdread4 libebackend-1_2-7 libe-book-0_1-1 libebook-1_2-14 libebook-contacts-1_2-0 libecal-1_2-16 libedata-book-1_2-20 libedata-cal-1_2-23 libedataserver-1_2-18 libenca0
> libetonyek-0_1-1 libevdocument3-4 libevview3-3 libexempi3 libexiv2-13 libexttextcat libexttextcat-2_0-0 libfbembed2_5 libfonts libformula libfreehand-0_1-1 libgdata19 libgdm1 libgee-0_8-2
> libgeocode-glib0 libgfbgraph-0_2-0 libgjs0 libGLEW1_10 libgltf-0_0-0 libGLU1 libgme0 libgmime-2_6-0 libgnome-bluetooth13 libgnome-desktop-3_0-common libgnome-desktop-3-10 libgnomekbd
> libgnomesu libgnomesu0 libgom-1_0-0 libgrilo-0_2-1 libgrlnet-0_2-0 libgrlpls-0_2-0 libgsf-1-114 libgsm1 libgssdp-1_0-3 libgstallocators-1_0-0 libgstbadbase-1_0-0 libgstbadvideo-1_0-0
> libgstbasecamerabinsrc-1_0-0 libgstcodecparsers-1_0-0 libgstgl-1_0-0 libgstmpegts-1_0-0 libgstphotography-1_0-0 libgstrtp-1_0-0 libgstrtsp-1_0-0 libgstsdp-1_0-0 libgsystem0
> libgtksourceview-3_0-1 libgtop-2_0-10 libgupnp-1_0-4 libgupnp-av-1_0-2 libgupnp-dlna-2_0-3 libgupnp-dlna-backend-gstreamer libgusb2 libgweather-3-6 libgweather-data libgxps2 libhyphen0
> libibus-1_0-5 libical1 libinput5 libiptcdata libiptcdata0 libixion-0_8-0 libjack0 libjavascriptcoregtk-4_0-18 liblangtag1 liblayout libloader liblouis2 liblpsolve55-0 liblrdf2
> libmbim-glib0 libmediaart-1_0-0 libmm-glib0 libmms0 libmozjs-24 libmspub-0_1-1 libmusicbrainz5-0 libmutter0 libmwaw-0_3-3 libmythes-1_2-0 libnautilus-extension1 libndp0 libneon27
> libnewt0_52 libnm-glib4 libnm-glib-vpn1 libnm-gtk0 libnm-util2 liboauth0 libodfgen-0_1-1 libofa0 libopenal1 libopus0 liborcus-0_8-0 libosinfo libosinfo-1_0-0 libpagemaker-0_0-0
> libportaudio2 libproxy1-config-gnome3 libproxy1-networkmanager libpulse-mainloop-glib0 libqmi-glib1 libqmi-tools libquvi libquvi-scripts libraptor2-0 librasqal3 librdf0 libreoffice
> libreoffice-base libreoffice-branding-upstream libreoffice-calc libreoffice-draw libreoffice-filters-optional libreoffice-icon-theme-breeze libreoffice-icon-theme-galaxy
> libreoffice-icon-theme-hicontrast libreoffice-icon-theme-sifr libreoffice-icon-theme-tango libreoffice-impress libreoffice-l10n-en libreoffice-mailmerge libreoffice-math libreoffice-pyuno
> libreoffice-share-linker libreoffice-templates-en libreoffice-templates-labels-a4 libreoffice-templates-labels-letter libreoffice-templates-presentation-layouts libreoffice-writer
> librepository librevenge-0_0-0 libserializer libslang2 libSoundTouch0 libspandsp2 libspeechd2 libstartup-notification-1-0 libtag1 libtag_c0 libtelepathy-logger3 libtotem-plparser18
> libtracker-common-1_0 libtracker-control-1_0-0 libtracker-miner-1_0-0 libtracker-sparql-1_0-0 libvdpau1 libvisio-0_1-1 libvte-2_91-0 libwacom2 libwacom-data libwavpack1 libwayland-egl1
> libwebkit2gtk3-lang libwebkit2gtk-4_0-37 libwnck-3-0 libwpd-0_10-10 libwpg-0_3-3 libwps-0_4-4 libxcb-xf86dri0 libxklavier16 libXRes1 libxslt-tools libzapojit-0_0-0 lua luasocket
> Mesa-demo-x mobile-broadband-provider-info ModemManager mutter mutter-data myspell-dictionaries myspell-en myspell-lightproof-en nautilus nautilus-extension-tracker-tags NetworkManager
> NetworkManager-gnome openal-soft orca pentaho-libxml pentaho-reporting-flow-engine polkit-gnome python3 python3-atspi python3-brlapi python3-gobject python3-gobject-cairo python3-louis
> python3-pip python3-setuptools python3-speechd rp-pppoe sac sbc shared-color-profiles speech-dispatcher speech-dispatcher-module-espeak sushi tcl totem-pl-parser tracker
> tracker-miner-files typelib-1_0-AccountsService-1_0 typelib-1_0-Atspi-2_0 typelib-1_0-Caribou-1_0 typelib-1_0-Clutter-1_0 typelib-1_0-ClutterGst-2_0 typelib-1_0-Cogl-1_0
> typelib-1_0-CoglPango-1_0 typelib-1_0-EvinceDocument-3_0 typelib-1_0-EvinceView-3_0 typelib-1_0-Gck-1 typelib-1_0-Gcr-3 typelib-1_0-GData-0_0 typelib-1_0-Gdm-1_0 typelib-1_0-GjsPrivate-1_0
> typelib-1_0-GnomeBluetooth-1_0 typelib-1_0-GnomeDesktop-3_0 typelib-1_0-Goa-1_0 typelib-1_0-Gst-1_0 typelib-1_0-GstAudio-1_0 typelib-1_0-GstPbutils-1_0 typelib-1_0-GstTag-1_0
> typelib-1_0-GstVideo-1_0 typelib-1_0-GSystem-1_0 typelib-1_0-GtkClutter-1_0 typelib-1_0-GtkSource-3_0 typelib-1_0-IBus-1_0 typelib-1_0-JavaScriptCore-3_0 typelib-1_0-JavaScriptCore-4_0
> typelib-1_0-Json-1_0 typelib-1_0-Meta-3_0 typelib-1_0-NetworkManager-1_0 typelib-1_0-NMClient-1_0 typelib-1_0-NMGtk-1_0 typelib-1_0-Rest-0_7 typelib-1_0-Soup-2_4
> typelib-1_0-TelepathyGlib-0_12 typelib-1_0-TelepathyLogger-0_2 typelib-1_0-Tracker-1_0 typelib-1_0-TrackerControl-1_0 typelib-1_0-UpowerGlib-1_0 typelib-1_0-WebKit2-4_0
> typelib-1_0-WebKit-3_0 typelib-1_0-Wnck-3_0 typelib-1_0-Xkl-1_0 typelib-1_0-Zpj-0_0 unoconv usb_modeswitch usb_modeswitch-data webkit2gtk-4_0-injected-bundles xbrlapi xerces-j2-xml-apis
> xorg-x11-server-extra zenity zip

> The following 34 recommended packages were automatically selected:

> avahi-autoipd brltty clutter-lang dleyna-server dnsmasq espeak evolution-data-server-lang fortune gdm gnome-clocks gnome-control-center gnome-control-center-user-faces gnome-online-miners
> gnome-shell-browser-plugin gnome-shell-search-provider-documents grilo-plugins libqmi-tools libwebkit2gtk3-lang ModemManager myspell-lightproof-en nautilus NetworkManager
> NetworkManager-gnome openal-soft orca python3-pip rp-pppoe sbc speech-dispatcher tracker tracker-miner-files unoconv usb_modeswitch webkit2gtk-4_0-injected-bundles

> 379 new packages to install.

> Overall download size: 127.6 MiB. Already cached: 80.4 MiB After the operation, additional 703.2 MiB will be used.
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

Next, ensure the "Enable Taskbar" option is checked

_click the "Next" button_

Yay! Elegant desktop environment. Ok now that we're FINALLY on the same page...

Next to the chameleon icon in your taskbar is a picture of what resembles a computer screen

_click that_

(If you aren't sure, if you pause the cursor of the picture, it should show a tooltip that says "Terminology".)

# Now onto the actual show:

In the newly created terminal screen enter:

`sudo zypper install git`

(if prompted, type in your root password and hit enter)

_hit enter_

you should see something similiar to:

> Loading repository data...

> Reading installed packages...

> Resolving package dependencies...

> The following 21 NEW packages are going to be installed:

> cvs cvsps git git-core git-cvs git-email git-gui gitk git-svn git-web libapr1 libapr-util1 libserf-1-1 perl-Authen-SASL perl-Error perl-Net-SMTP-SSL subversion subversion-bash-completion subversion-perl tk
> xhost

> The following 9 recommended packages were automatically selected:

> git-cvs git-email git-gui gitk git-svn git-web perl-Authen-SASL perl-Net-SMTP-SSL subversion-bash-completion

> The following package is suggested, but will not be installed:

> git-daemon

> 21 new packages to install.

> Overall download size: 9.6 MiB. Already cached: 0 B After the operation, additional 36.9 MiB will be used.

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

`cd ~/`

_hit enter_

`git clone git://github.com/cantino/huginn.git`

_hit enter_

`cd ..`

_hit enter_

You should be back at /home/<your username> - (or another way of writing it: ~/)

##Installing MySQL (MariaDB)

Before entering proceeding further, be ready to answer questions about the MySQL database install that is required
questions such as:

- What you want your database root account's password to be

Now enter the following:

`sudo zypper install mysql`

(if prompted, type in your root password and hit enter)

_hit enter_

You should now see something along the lines of:

> Retrieving repository 'openSUSE-13.2-Update' metadata
> ..........................................................................................................................
> ...................................[done]

> Building repository 'openSUSE-13.2-Update' cache
> ..........................................................................................................................
> ........................................[done]

> Loading repository data...

> Reading installed packages...

> 'mysql' not found in package names. Trying capabilities.

> Resolving package dependencies...

> The following 9 NEW packages are going to be installed:

> libjemalloc1 libmysqlclient18 libmysqlclient_r18 libmysqlcppconn6 libreadline5 libreoffice-base-drivers-mysql mariadb mariadb-client mariadb-errormessages

> 9 new packages to install.

> Overall download size: 11.2 MiB. Already cached: 0 B After the operation, additional 107.0 MiB will be used.

> Continue? [y/n/? shows all options] (y):

_hit enter_

> You may eventually see something like this:

> Retrieving package libjemalloc1-3.6.0-2.1.2.x86_64 (1/9), 105.4 KiB (266.8 KiB unpacked)

> Retrieving: libjemalloc1-3.6.0-2.1.2.x86_64.rpm ...................................................................................................................................................................[done]

> Retrieving package libmysqlcppconn6-1.1.2-6.2.2.x86_64 (2/9), 165.0 KiB (668.6 KiB unpacked)

> Retrieving: libmysqlcppconn6-1.1.2-6.2.2.x86_64.rpm ...............................................................................................................................................................[done]

> Retrieving package libreadline5-5.2-133.1.2.x86_64 (3/9), 96.6 KiB (295.8 KiB unpacked)

> Retrieving: libreadline5-5.2-133.1.2.x86_64.rpm ...................................................................................................................................................................[done]

> Retrieving package libmysqlclient18-10.0.25-2.24.1.x86_64 (4/9), 557.1 KiB ( 3.3 MiB unpacked)

> Retrieving: libmysqlclient18-10.0.25-2.24.1.x86_64.rpm ............................................................................................................................................................[done]

> Retrieving package mariadb-errormessages-10.0.25-2.24.1.x86_64 (5/9), 184.5 KiB ( 1.9 MiB unpacked)

> Retrieving: mariadb-errormessages-10.0.25-2.24.1.x86_64.rpm .......................................................................................................................................................[done]

> Retrieving package libmysqlclient_r18-10.0.25-2.24.1.x86_64 (6/9), 31.7 KiB ( 0 B unpacked)

> Retrieving: libmysqlclient_r18-10.0.25-2.24.1.x86_64.rpm ..........................................................................................................................................................[done]

> Retrieving package mariadb-client-10.0.25-2.24.1.x86_64 (7/9), 874.2 KiB ( 19.9 MiB unpacked)

> Retrieving: mariadb-client-10.0.25-2.24.1.x86_64.rpm ..............................................................................................................................................................[done]

> Retrieving package libreoffice-base-drivers-mysql-5.0.6.3-31.3.x86_64 (8/9), 388.5 KiB (857.5 KiB unpacked)

> Retrieving: libreoffice-base-drivers-mysql-5.0.6.3-31.3.x86_64.rpm ................................................................................................................................................[done]

> Retrieving package mariadb-10.0.25-2.24.1.x86_64 (9/9), 8.8 MiB ( 79.8 MiB unpacked)

> Retrieving: mariadb-10.0.25-2.24.1.x86_64.rpm .........................................................................................................................................................[done (2.3 MiB/s)]

> Checking for file conflicts: ......................................................................................................................................................................................[done]

> (1/9) Installing: libjemalloc1-3.6.0-2.1.2 ........................................................................................................................................................................[done]

> (2/9) Installing: libmysqlcppconn6-1.1.2-6.2.2 ....................................................................................................................................................................[done]

> (3/9) Installing: libreadline5-5.2-133.1.2 ........................................................................................................................................................................[done]

> (4/9) Installing: libmysqlclient18-10.0.25-2.24.1 .................................................................................................................................................................[done]

> (5/9) Installing: mariadb-errormessages-10.0.25-2.24.1 ............................................................................................................................................................[done]

> (6/9) Installing: libmysqlclient_r18-10.0.25-2.24.1 ...............................................................................................................................................................[done]

> (7/9) Installing: mariadb-client-10.0.25-2.24.1 ...................................................................................................................................................................[done]

> Additional rpm output:

> usermod: no changes

> (8/9) Installing: libreoffice-base-drivers-mysql-5.0.6.3-31.3 .....................................................................................................................................................[done]

> (9/9) Installing: mariadb-10.0.25-2.24.1 ..........................................................................................................................................................................[done]

> Additional rpm output:

> usermod: no changes

> Update notifications were received from the following packages:

> mariadb-10.0.25-2.24.1.x86_64 (/var/adm/update-messages/mariadb-10.0.25-2.24.1)

> View the notifications now? [y/n] (n):

You can type the letter y and <hit enter> if you like. If you do, you'll likely see something like this:
(Use arrows or pgUp/pgDown keys to scroll the text by lines or pages.)

> Message from package mariadb:
> You just installed MySQL server for the first time.

> You can start it using:

> rcmysql start

> During first start empty database will be created for your automatically.

> PLEASE REMEMBER TO SET A PASSWORD FOR THE MariaDB root USER !

> To do so, start the server, then issue the following commands:

> '/usr/bin/mysqladmin' -u root password 'new-password'

> '/usr/bin/mysqladmin' -u root -h <hostname> password 'new-password'

> Alternatively you can run:

> '/usr/bin/mysql_secure_installation'

> which will also give you the option of removing the test

> databases and anonymous user created by default. This is

> strongly recommended for production servers.

> -----------------------------------------------------------------------------`

###Start the newly installed MySQL (MariaDB) service

`sudo service mysql start`

_hit enter_

(if prompted, type in your root password and hit enter)

Now enter:

`/usr/bin/mysql_secure_installation`

_hit enter_

You'll see something like this:

>      NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB

>           SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

>     In order to log into MariaDB to secure it, we'll need the current

>     password for the root user.  If you've just installed MariaDB, and

>     you haven't set the root password yet, the password will be blank,

>     so you should just press enter here.

>     Enter current password for root (enter for none):

_hit enter_

You'll see:

>     OK, successfully used password, moving on...

>     Setting the root password ensures that nobody can log into the MariaDB

>     root user without the proper authorisation.

>     Set root password? [Y/n]

_Type the letter y_

_hit enter_

_enter your new database's root password_ (**Make sure it's a GOOD password! Uppercase, Lowercase, Numbers, Symbols, and try for something like 12 characters, longer is better! One note: DO NOT use a $ symbol for the password, it will throw the bundle exec rake db:create task off much much later on in the process!!!!**)

_hit enter_

_reenter that password again_

_hit enter_

You'll now see:

> Password updated successfully!

> Reloading privilege tables..

> ... Success!

> By default, a MariaDB installation has an anonymous user, allowing anyone

> to log into MariaDB without having to have a user account created for

> them. This is intended only for testing, and to make the installation

> go a bit smoother. You should remove them before moving into a

> production environment.

> Remove anonymous users? [Y/n]

_type the letter y_

_hit enter_

You'll now see:

> ... Success!

> Normally, root should only be allowed to connect from 'localhost'. This
> ensures that someone cannot guess at the root password from the network.

> Disallow root login remotely? [Y/n]

NOTE: disallowing root connections is strongly recommended, however if you are installing this on a remote machine, not having a remote admin ability can be one of the most obnoxious things to deal with when troubleshooting or doing development work that will be using the same database because you then have to fight (maybe they've made it easier since I last remember) MySQL to allow remote root connection. That said, securing a remote root login ability can be challenging, and having it enabled presents a -MAJOR- security risk, so if you know you'll be able to function without it

**type the letter y**

_hit enter_

You should then see:

> ... Success!

> By default, MariaDB comes with a database named 'test' that anyone can access. This is also intended only for testing, and should be removed before moving into a production environment.

> Remove test database and access to it? [Y/n]

_Type the letter y_

_hit enter_

Next, you'll see:

> - Dropping test database...

> ... Success!

> - Removing privileges on test database...

> ... Success!

> Reloading the privilege tables will ensure that all changes made so far

> will take effect immediately.

> Reload privilege tables now? [Y/n]

_Type the letter y_
_hit enter_

You'll now see:

> ... Success!

> Cleaning up...

> All done! If you've completed all of the above steps, your MariaDB

> installation should now be secure.

> Thanks for using MariaDB!

##Install MySQL2

###Install the libmysqlclient-dev

At the terminal window enter the following:

`sudo zypper install libmysqlclient-dev`

_hit enter_

_hit enter_

###Install the MySQL2 gem

At the terminal window enter the following:

`gem install mysql2 -v '0.3.20'`

_hit enter_

You'll see:

>     Building native extensions.  This could take a while...

>     Successfully installed mysql2-0.3.20

>     Parsing documentation for mysql2-0.3.20

>     Installing ri documentation for mysql2-0.3.20

>     Done installing documentation for mysql2 after 0 seconds

>     1 gem installed

(Despite it saying it could take a while, it really actually didn't; at least for me)

##Setting up your Ruby environment (using rvm)

This is where things get dicey. At this point, ruby IS actually already installed on your system. For OpenSUSE 13.2, as of 07/05/2016 at 11:03PM EDT, even with online repositories enabled during install of the distro, it is NOT at the version you need to be at. The novice guide says Ruby 2+, while the distro has Ruby at a version 2+, it is not sufficient.

Enter the following:

`ruby --version`

_hit enter_

You should see the following:

> ruby 2.1.3p242 (2014-09-19 revision 47630) [x86_64-linux-gnu]

Now do the same for but for gem

Enter the following:

`gem --version`

_hit enter_

You should see the following:

> 2.2.2

(we shouldn't need to upgrade Gem though -- this is just for "thoroughness")

Brief terminology reference:

Ruby is a language

Gems are Ruby packages (think of them as like libraries)

gem (first letter lowercase and no 's' on the end) is a package manager (technically it's called RubyGems, but you use the gem command to use it) used to install Gems

bundler is the name of the program/utility you use to build packages

bundle is the command used to build packages

Two ways of proceeding:

1 - A system wide install of an updated Ruby version

2 - (Recommended): RVM (Ruby Version Management) - Many community members go this route; thus, it is recommended as individuals are more likely to have direct experience troubleshooting issues specific with dealing with RVM than system-wide installs that can vary.

    From the RVM site: "RVM is a command-line tool which allows you to easily install, manage, and work with multiple ruby environments from interpreters to sets of gems."

###If you want to install a system-wide updated version of Ruby

Download Ruby source

At the terminal prompt enter:

`mkdir Downloads`

_hit enter_

`cd Downloads`

_hit enter_

The file can be found at: http://www.ruby-lang.org/en/downloads/

The direct link is: https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.1.tar.gz

Either download into your downloads folder (which should be ~/<your username here>/Downloads) using your web browser

or you can shortcut loading the window by entering the following into the terminal window:

`wget https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.1.tar.gz`

_hit enter_

Regardless of whether you ran downloaded using the browser or you used wget enter the following into the terminal window:

`openssl dgst -sha256 ruby-2.3.1.tar.gz`

_hit enter_

the hexadecimal string that is output from this command should match the listing on the web page; if it doesn't something's wrong. Try redownloading it and reperforming this step again.

Presently at 07/06/2016 2:39AM EDT my output shows: SHA256(ruby-2.3.1.tar.gz)= b87c738cb2032bf4920fef8e3864dc5cf8eae9d89d8d523ce0236945c5797dcd

(but you should verify it yourself though anyway)

if it matches proceed.

Enter the following:

`tar xzvf ./ruby-2.3.1.tar.gz`

_hit enter_

wait for it to unpack

Next enter:

`cd ruby-2.3.1`

_hit enter_

Now enter:

`make`

_hit enter_

wait for that to finish then enter:

`sudo make install`

_hit enter_

(if prompted, type in your root password and hit enter)

###If you are going the rvm route

You can get the latest commands to install rvm the "secure" way by visiting [https://rvm.io/rvm/security](https://rvm.io/rvm/security) in a web browser

As of 07/06/2016 at 2:47AM EDT the commands are as follows:

(Due to the nature that there is a key involved, it is HIGHLY recommended you get this key DIRECTLY from their site)

In your terminal window, enter the following:

`gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3`

_hit enter_

`pwd`

_hit enter_

Confirm your present working directory is ~/<your username>

(if not, enter cd ~/ and hit enter)

Next enter:

`\curl -O https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer`

_hit enter_

wait until this finishes then enter:

`\curl -O https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer.asc`

_hit enter_

wait until this finishes then enter:

`gpg --verify rvm-installer.asc &&`

_hit enter_

you will now see a > prompt (that's fine) now enter the following:

`bash rvm-installer stable`

_hit enter_

if you see the error: gpg: Signature made Thu 21 Jan 2016 02:38:21 PM EST using RSA key ID BF04FF17

gpg: Can't check signature: No public key

then enter the following:

`curl -sSL https://rvm.io/mpapis.asc | gpg --import -`

(yes the - at the end is meant to be there)

Now reenter the following:

`gpg --verify rvm-installer.asc && bash rvm-installer stable`

_hit enter_

You will likely see it say the certificate is expired. I suppose that's fine. It is kind've weird though their certificate
is expired...

After the validation of the key, you should see the following right after it:

> Installing RVM to /home/<your username>/.rvm/

>     Adding rvm PATH line to /home/<your username>/.profile /home/<your username>/.mkshrc /home/<your username>/.bashrc /home/<your username>/.zshrc.

>     Adding rvm loading line to /home/<your username>/.profile /home/<your username>/.bash_profile /home/<your username>/.zlogin.

> Installation of RVM in /home/<your username>/.rvm/ is almost complete:

> - To start using RVM you need to run `source /home/<your username>/.rvm/scripts/rvm`

>     in all your open shell windows, in rare cases you need to reopen all shell windows.

> # <your username>,

> #

> # Thank you for using RVM!

> # We sincerely hope that RVM helps to make your life easier and more enjoyable!!!

> #

> # ~Wayne, Michal & team.

> In case of problems: https://rvm.io/help and https://twitter.com/rvm_io

Now enter the following:

`source /home/<your username>/.rvm/scripts/rvm`

_hit enter_

You need to do this because rvm is being defined as a Bash function, and without the function in place you'll get the error:

    > If 'rvm' is not a typo you can use command-not-found to lookup the package that contains it, like this:

>     		cnf rvm

So go ahead and run it.

You will need to reopen a new shell so close out the existing shell terminal you have open, and reopen a new one.

Next enter the following:

`rvm install 2.3.1`

_hit enter_

You should see something to the effect of:

    > Searching for binary rubies, this might take some time.

>     No binary rubies available for: opensuse/13.2/x86_64/ruby-2.3.1.

>     Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.

>     Checking requirements for opensuse.

>     Installing requirements for opensuse.

>     Updating systemroot password required for 'zypper --gpg-auto-import-keys refresh': ..-

>     ..

>     Installing required packages: patch, automake, bison, libtool, m4, make, patch, gdbm-devel, glibc-devel, libffi-devel, libopenssl-devel, readline-devel, zlib-devel, libdb-4_5, sqlite3-devel, gcc, gcc-c++, libyaml-devel...............

>     Requirements installation successful.

>     Installing Ruby from source to: /home/<your username>/.rvm/rubies/ruby-2.3.1, this may take a while depending on your cpu(s)...

>     ruby-2.3.1 - #downloading ruby-2.3.1, this may take a while depending on your connection...

>       % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current

>         	                         Dload  Upload   Total   Spent    Left  Speed

>     100 13.7M  100 13.7M    0     0   843k      0  0:00:16  0:00:16 --:--:-- 2341k

>     No checksum for downloaded archive, recording checksum in user configuration.

>     ruby-2.3.1 - #extracting ruby-2.3.1 to /home/<your username>/.rvm/src/ruby-2.3.1....

>     ruby-2.3.1 - #configuring..........................................................

>     ruby-2.3.1 - #post-configuration..

>     ruby-2.3.1 - #compiling.................................................................................

>     ruby-2.3.1 - #installing..............

>     ruby-2.3.1 - #making binaries executable..

>     Installed rubygems 2.5.1 is newer than 2.4.8 provided with installed ruby, skipping installation, use --force to force installation.

>     ruby-2.3.1 - #gemset created /home/<your username>/.rvm/gems/ruby-2.3.1@global

>     ruby-2.3.1 - #importing gemset /home/<your username>/.rvm/gemsets/global.gems...............................................

>     ruby-2.3.1 - #generating global wrappers........

>     ruby-2.3.1 - #gemset created /home/<your username>/.rvm/gems/ruby-2.3.1

>     ruby-2.3.1 - #importing gemsetfile /home/<your username>/.rvm/gemsets/default.gems evaluated to empty gem list

>     ruby-2.3.1 - #generating default wrappers........

>     ruby-2.3.1 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).

>     Install of ruby-2.3.1 - #complete

>     Ruby was built without documentation, to build it run: rvm docs generate-ri

(NOTE: On the line that says: Updating systemroot password required for 'zypper --gpg-auto-import-keys refresh': ..-

The 7th line down. You may need to enter your password. I say may because I'm not sure, and I'm not sure, because the line
breaking got messed up. I entered mine and it didn't echo which means I must've been in a password text input mode/field.

I suspect if you literally just entered your root password seconds ago, it may report it needs the password but execute
because it's within the few seconds that the root authentication window is still open)

wait for that to finish

Next enter:

`/bin/bash --login`

_hit enter_

`rvm use 2.3.1 --default`

_hit enter_

`rvm list`

`hit enter`

You should see:

    > RVM used your Gemfile for selecting Ruby, it is all fine - Heroku does that too,

>     you can ignore these warnings with 'rvm rvmrc warning ignore /home/<your username>/huginn/Gemfile'.

>     To ignore the warning for all files run 'rvm rvmrc warning ignore allGemfiles'.

>     Unknown ruby interpreter version (do not know how to handle): [2.0.0,RUBY_VERSION].max.

>     rvm rubies

>     =* ruby-2.3.1 [ x86_64 ]

>     # => - current

>     # =* - current && default

>     #  * - default

Next enter:

`ruby --version`

_hit enter_

You should see:

    > ruby 2.3.1p112 (2016-04-26 revision 54768) [x86_64-linux]

This confirms that our Ruby environment is pointed at our local setup for our current user and the particular version of Ruby!

Coming down to the home stretch!

Now enter:

`gem install rake bundler`

(You should NOT need root for this since it is our own user's Ruby environment not the system-wide one. If you need root password, you likely did something wrong; go back and check the commands.)

_hit enter_

`gem install mysql2 -v '0.3.20'`

_hit enter_

`cd ~/`

_hit enter_

`cd huginn*`

_hit enter_

`bundle`

_hit enter_

You should see:

> Fetching gem metadata from https://rubygems.org/

> Fetching version metadata from https://rubygems.org/

> Fetching dependency metadata from https://rubygems.org/

> Resolving dependencies.......

> Using rake 10.5.0

> Using ace-rails-ap 2.0.1

> Using i18n 0.7.0

> Using json 1.8.3

> Using minitest 5.8.4

> Using thread_safe 0.3.5

> Using builder 3.2.2

> Using erubis 2.7.0

> Using mini_portile2 2.1.0

> Using pkg-config 1.1.7

> Using rack 1.6.4

> Using mime-types 2.99.1

> Using arel 6.0.3

> Using addressable 2.3.8

> Using extlib 0.9.16

> Using multi_json 1.11.2

> Using jmespath 1.1.3

> Using bcrypt 3.1.10

> Using coderay 1.1.0

> Using debug_inspector 0.0.2

> Using bundler 1.12.5

> Using thor 0.19.1

> Using concurrent-ruby 1.0.1

> Using buftok 0.2.0

> Using byebug 8.2.5

> Using colorize 0.7.7

> Using net-ssh 2.9.2

> Using rspec-support 3.2.2

> Using diff-lcs 1.2.5

> Using chronic 0.10.2

> Using cliver 0.3.2

> Using coffee-script-source 1.10.0

> Using execjs 2.6.0

> Using cookiejar 0.3.2

> Using unf_ext 0.0.7.1

> Using netrc 0.10.3

> Using docile 1.1.5

> Using simplecov-html 0.9.0

> Using tins 1.10.1

> Using safe_yaml 1.0.4

> Using daemons 1.1.9

> Using database_cleaner 1.5.3

> Using orm_adapter 0.5.0

> Using dotenv 2.0.1 from source at `vendor/gems/dotenv-2.0.1`

> Using hashie 2.0.5

> Using oauth 0.4.7

> Using eventmachine 1.0.7

> Using http_parser.rb 0.6.0

> Using equalizer 0.0.11

> Using polyglot 0.3.5

> Using ffi 1.9.10

> Using evernote-thrift 1.25.1

> Using multipart-post 2.0.0

> Using hpricot 0.8.6

> Using simple-rss 1.3.1

> Using sass 3.4.14

> Using formatador 0.2.5

> Using jwt 1.4.1

> Using retriable 2.0.2

> Using uuidtools 2.1.5

> Using rb-fsevent 0.9.7

> Using lumberjack 1.0.10

> Using nenv 0.2.0

> Using shellany 0.0.1

> Using method_source 0.8.2

> Using slop 3.6.0

> Using guard-compat 1.2.1

> Using haversine 0.3.0

> Using multi_xml 0.5.5

> Using mimemagic 0.3.1

> Using kgio 2.9.3

> Using kramdown 1.3.3

> Using libv8 3.16.14.13

> Using liquid 3.0.6

> Using systemu 2.6.4

> Using mini_magick 4.2.3

> Using mqtt 0.3.1

> Using mysql2 0.3.20

> Using naught 1.0.0

> Using net-ftp-list 3.2.8

> Using websocket-extensions 0.1.2

> Using raindrops 0.13.0

> Using ref 2.0.0

> Using rr 1.1.2

> Using tilt 1.4.1

> Using simple_oauth 0.3.1

> Using slack-notifier 1.0.0

> Using string-scrub 0.0.5

> Using vcr 2.9.2

> Using xmpp4r 0.5.6

> Using tzinfo 1.2.2

> Using memoizable 0.4.2

> Using nokogiri 1.6.8

> Using rack-test 0.6.3

> Using warden 1.2.4

> Using rack-livereload 0.3.16

> Using mail 2.6.3

> Using launchy 2.4.2

> Using autoparse 0.3.3

> Using geokit 1.8.5

> Using jsonpath 0.5.7

> Using aws-sdk-core 2.2.15

> Using better_errors 1.1.0

> Using binding_of_caller 0.7.2

> Using huginn_agent 0.4.0

> Using select2-rails 3.5.9.3

> Using sprockets 3.5.2

> Using net-scp 1.2.1

> Using rspec-core 3.2.1

> Using rspec-expectations 3.2.0

> Using rspec-mocks 3.2.1

> Using delorean 2.1.0

> Using coffee-script 2.4.1

> Using uglifier 2.7.2

> Using unf 0.1.4

> Using simplecov 0.9.2

> Using term-ansicolor 1.3.2

> Using crack 0.4.2

> Using dotenv-rails 2.0.1 from source at `vendor/gems/dotenv-2.0.1`

> Using foreman 0.63.0

> Using omniauth 1.2.2

> Using dropbox-api 0.4.2

> Using em-socksify 0.3.0

> Using em-websocket 0.5.1

> Using http 0.6.4

> Using treetop 1.5.3

> Using ethon 0.7.1

> Using rb-inotify 0.9.5

> Using evernote_oauth 0.2.3

> Using faraday 0.9.1

> Using feed-normalizer 1.5.2

> Using font-awesome-sass 4.3.2.1

> Using twilio-ruby 3.11.6

> Using notiffany 0.0.8

> Using pry 0.10.3

> Using httparty 0.13.7

> Using macaddr 1.7.1

> Installing websocket-driver 0.6.3 with native extensions

> Installing unicorn 4.9.0 with native extensions

> Installing therubyracer 0.12.2 with native extensions

> Using twitter-stream 0.1.15 from git://github.com/cantino/twitter-stream.git (at huginn@f7e7edb)

> Installing activesupport 4.2.5.2

> Installing rufus-scheduler 3.0.9

> Installing loofah 2.0.3

> Installing xpath 2.0.0

> Installing letter_opener 1.4.1

> Installing sshkit 1.7.1

> Installing rspec-collection_matchers 1.1.2

> Installing rspec 3.2.0

> Installing domain_name 0.5.24

> Installing webmock 1.17.4

> Installing omniauth-oauth 1.0.1

> Installing em-http-request 1.1.2

> Installing erector 0.10.0

> Installing typhoeus 0.6.9

> Installing listen 3.0.5

> Using faraday_middleware 0.10.0 from git://github.com/lostisland/faraday_middleware.git (at master@c5836ae)

> Installing forecast_io 2.0.0

> Installing signet 0.5.1

> Installing oauth2 0.9.4

> Installing twitter 5.14.0

> Installing pry-byebug 3.3.0

> Installing pry-rails 0.3.4

> Installing hipchat 1.2.0

> Installing httmultiparty 0.3.16

> Installing wunderground 1.2.0

> Installing uuid 2.3.7

> Installing rails-deprecated_sanitizer 1.0.3

> Installing globalid 0.3.6

> Installing activemodel 4.2.5.2

> Installing delayed_job 4.1.1

> Installing shoulda-matchers 3.0.0

> Installing rails-html-sanitizer 1.0.3

> Installing capybara 2.6.2

> Installing capistrano 3.4.0

> Installing rspec-html-matchers 0.7.0

> Installing http-cookie 1.0.2

> Installing omniauth-dropbox 0.2.0

> Installing omniauth-evernote 1.2.1

> Installing omniauth-tumblr 1.1

> Installing omniauth-twitter 1.0.1

> Installing guard 2.13.0

> Using tumblr_client 0.8.5 from git://github.com/tumblr/tumblr_client.git (at master@0c59b04)

> Installing google-api-client 0.7.1

> Installing omniauth-oauth2 1.1.2

> Installing hypdf 1.0.10

> Installing ruby-growl 4.1

> Installing rails-dom-testing 1.0.7

> Installing activejob 4.2.5.2

> Installing activerecord 4.2.5.2

> Installing protected_attributes 1.0.8

> Installing capybara-select2 1.0.1

> Installing poltergeist 1.8.1

> Installing capistrano-bundler 1.1.4

> Installing rest-client 1.8.0

> Installing guard-livereload 2.5.1

> Installing guard-rspec 4.6.4

> Installing omniauth-37signals 1.0.5

> Using omniauth-wunderlist 0.0.1 from git://github.com/wunderlist/omniauth-wunderlist.git (at d0910d0@d0910d0)

> Installing actionview 4.2.5.2

> Using delayed_job_active_record 4.1.0 from git://github.com/collectiveidea/delayed_job_active_record.git (at
> master@61e688e)

> Installing capistrano-rails 1.1.3

> Installing coveralls 0.7.12

> Installing rturk 2.12.1

> Using weibo_2 0.1.7 from git://github.com/cantino/weibo_2.git (at master@00e57d2)

> Installing actionpack 4.2.5.2

> Installing actionmailer 4.2.5.2

> Installing kaminari 0.16.1

> Installing railties 4.2.5.2

> Installing sprockets-rails 3.0.3

> Installing coffee-rails 4.1.1

> Installing responders 2.1.1

> Installing jquery-rails 3.1.3

> Installing letter_opener_web 1.3.0

> Installing quiet_assets 1.1.0

> Installing rspec-rails 3.2.1

> Installing spectrum-rails 1.3.4

> Installing rails 4.2.5.2

> Installing sass-rails 5.0.3

> Installing devise 3.5.4

> Installing bootstrap-kaminari-views 0.0.5

> Installing geokit-rails 2.0.1

> Bundle complete! 104 Gemfile dependencies, 222 gems now installed.

> Use `bundle show [gemname]` to see where a bundled gem is installed.

> Post-install message from rufus-scheduler:

> ---

> Thanks for installing rufus-scheduler 3.0.9

> It might not be 100% compatible with rufus-scheduler 2.x.

> If you encounter issues with this new rufus-scheduler, especially

> if your app worked fine with previous versions of it, you can

> A) Forget it and peg your Gemfile to rufus-scheduler 2.0.24

> and / or

> B) Take some time to carefully report the issue at

> https://github.com/jmettraux/rufus-scheduler/issues

> For general help about rufus-scheduler, ask via:

> http://stackoverflow.com/questions/ask?tags=rufus-scheduler+ruby

> Cheers.

> ---

>     Post-install message from capistrano:

> Capistrano 3.1 has some breaking changes. Please check the CHANGELOG: http://goo.gl/SxB0lr

> If you're upgrading Capistrano from 2.x, we recommend to read the upgrade guide: http://goo.gl/4536kB

> The `deploy:restart` hook for passenger applications is now in a separate gem called capistrano-passenger. Just add it to your Gemfile and require it in your Capfile.

(this will take a WHILE. Get a cup of coffee, put the TV on, relax a little; take a breather --you've earned it! Yeah -THAT- long :P )

Wait for it to finish then enter:

`cp .env.example .env`

_hit enter_

`rake secret`

_hit enter_

Select the string of hexadecimals and copy it to your clipboard

Now enter

`leafpad .env`

_hit enter_

locate the line that says APP_SECRET_TOKEN=REPLACE_ME_NOW!

highlight the text REPLACE_ME_NOW! and overwrite it with the string of hexadecimals you copied to your clipboard

also locate the line that say "DATABASE_PASSWORD" under the Database Setup section and add the database's root account
password between the quotes

Next locate the line that says "DATABASE_SOCKET=/tmp/mysql.sock" (also under the "Database Setup" section) and

either replace the part that says: /tmp/mysql.sock

    with: /var/run/mysql/mysql.sock

    or duplicate the line, comment out the original (by putting a # at the begining of the original line) and modify the duplicated line to the requested changes

Next locate the line that says "#DATABASE_ENCODING=utf8mb4" and remove the # at the begining of the line

Save the file and close leafpad

(Note: Get familiar with this .env file, you will likely be making many changes and tweaks as you continue to use Huginn and your needs change or develop)

Go back to the terminal window you were just working in

Now enter:

`gnomesu leafpad /etc/my.cnf`

(Enter your root password in the popup and hit enter)

Locate the line that starts with "# socket =" and delete the # at the very beginning of the line.

Save the file and close leafpad

Go back to the terminal window you were just working in and enter:

`sudo service mysql restart`

(If prompted, enter your root password and hit enter)

`bundle exec rake db:create`

_hit enter_

Provide the MySQL (MariaDB) database root password

_hit enter_

`bundle exec rake db:migrate`

_hit enter_

`bundle exec rake db:seed`

_hit enter_

_drum roll..._

now to actually cause it to run enter:

`bundle exec foreman start`

_hit enter_

Open a web browser and type in http://localhost:3000

log in with the username of admin and the password of password

Hopefully that completes your install. I don't know about you but I'm exhausted.

---

As an added bonus (perhaps this should be added to its own wiki, but for now I don't think there's really enough here to necessitate an entire wiki page -- if/when it does I'll move it out; unless someone thinks it should already?)

Some generic troubleshooting with Huginn

[This scenario entered on: 01/24/2016 12:46PM EST]

scenario: You attempt to start Huginn again and for whatever reason you get something along the lines of:

14:25:51 jobs.1 | /home/[username]/.rvm/gems/ruby-2.3.1/gems/activesupport-5.0.0.1/lib/active_support/dependencies.rb:293:in `require': incompatible library version - /home/[username]/.rvm/gems/ruby-2.3.1/gems/eventmachine-1.0.7/lib/rubyeventmachine.so (LoadError)

[...]

14:26:17 web.1 | exited with code 1
14:26:17 system | sending SIGTERM to all processes
14:26:17 jobs.1 | exited with code 1

It's possible you did a bundle update since you've last had Huginn running successfully, and because the Gemfile doesn't specify version numbers, breakage is most likely going to occur as time progresses and the many many dependencies Huginn uses gets updated over time. Either way, the culprit of this problem is, the Gemfile does not specify the version that Huginn needs and thus if an update is done then it just grabs the latest version.

Type in:
gem uninstall activesupport
<hit enter>

Type in:
bundler exec foreman start
<hit enter>

You should see a line that says something to the extent of:

"Could not find activesupport-5.0.0.1 in any of the sources"

Type in:
bundle install
<hit enter>

You should see a line in the output that says:

"Installing activesupport 5.0.0.1"

A dependency set to just grab the latest copy blindly.

You can try bringing all the other dependencies up to current version but you could wind up creating more breakage. If you want to chance it you can type in:

bundle update
<hit enter>

You should see a bunch of the packages say Installing <gem name> <version> (was <previously installed version>)

try running foreman again by typing:
bundler exec foreman start
<hit enter>

In that output you should see a message along the lines of:

04:23:40 web.1 | /home/[username]/.rvm/gems/ruby-2.3.1/gems/bundler-1.14.2/lib/bundler/runtime.rb:91:in `require': cannot load such file -- google/api_client (LoadError)

Where I went when working through this was I uninstalled bundler and reinstalled it to grab the latest version (I suppose there is an update command for the specific gem?)

Type in:
gem uninstall bundler

You'll get an output of a ton of gems that depend on bundler. That's fine, we're reinstalling it in a sec. anyhow.
so when you see:
"If you remove this gem, these dependencies will not be met.
Continue with Uninstall? [yN]"

Type in:
y
<hit enter>

Then you'll see:
"Remove executables:
bundle, bundler

in addition to the gem? [Yn]"

Type in:
y
<hit enter>

Then you'll see something along the lines of:

"Removing bundle
Removing bundler
Successfully uninstalled bundler-1.14.2"

Now type in:
gem install bundler
<hit enter>

Now try running Huggin again by typing:
bundler exec foreman start
<hit enter>

You'll likely still see the error about google-api-clients

If you go here and look at the comment:
https://github.com/gimite/google-drive-ruby/issues/167#issuecomment-147483919

You'll see there appears to be some breakage with the newer version.

If you go here:
https://github.com/google/google-api-ruby-client

You'll see this blurb:
"Migrating from 0.8.x

Version 0.9 is not compatible with previous versions. See MIGRATING for additional details on how to migrate to the latest version."

confirming it. If you go here:
https://github.com/google/google-api-ruby-client/blob/master/MIGRATING.md

You'll see this blurb:
"Migrating from version 0.8.x to 0.9

Many changes and improvements have been made to the google-api-ruby-client library to bring it to 0.9. If you are starting a new project or haven't used this library before version 0.9, see the README to get started as you won't need to migrate anything.

Code written against the 0.8.x version of this library will not work with the 0.9 version without modification."

Oh boy; that's some pretty strong verbiage. We're not just talking small changes... Notice the word Many and the outright strong statement that previous code will not work without modification.

So type in:
gem uninstall google-api-client
<hit enter>

remove each version that is above 0.8.x

Now, technically, it should work. But I'm going to have you modify your gemfile so it's forced to the latest version that still works.

Go into your Huginn's root folder and open the file titled Gemfile in your favorite text editor and locate the line that states:
gem "google-api-client", require: 'google/api_client'

make the line:
#gem "google-api-client", require: 'google/api_client'

and, to that section, add the line:
gem 'google-api-client', '0.8.2', require: 'google/api_client'

Now save the file and exit

Now type in:
bundler update
<hit enter>

In my output of issuing that command I saw the line:
Installing google-api-client 0.8.2 (was 0.9.23)

You should see something similar.

Now try running Huginn again by typing:
bundler exec foreman start
<hit enter>

In that output, you will probably see the line:
04:51:46 web.1 | /home/[username]/.rvm/gems/ruby-2.3.1/gems/binding_of_caller-0.7.2/lib/binding_of_caller/mri2.rb:21:in `callers': uninitialized constant RubyVM::DebugInspector (NameError)

_sigh_ this is endless... A few lines down you see mention of better_errors, you can try uninstalling that -- that's what I did but it didn't fix it. I believe it wasn't until I focused on DebugInspector that was the final bit of the fix.

So type in:
gem uninstall debug_inspector

Say y to removing the gem, and say y to continue with uninstall, you know the drill by now...

Now type in:
bundle
<hit enter>

In that output you should see something alongs the lines of:
"Installing debug_inspector 0.0.2 with native extensions"

Now try running Huginn again by typing:
bundler exec foreman start
<hit enter>

Huginn should now start... yay.

01/24/2016 12:46PM EST: Formatting for this scenario needs to be done

Scenario: You power on your huginn server/workstation/vm from cold and you use ruby --version and you get something that states you're using ruby version 2.1.3 (NOT 2.3.1)

Fix: This is a pretty simply fix. in your terminal window enter the following:

`/bin/bash --login`

_hit enter_

`rvm --use 2.3.1 --default`

_hit enter_

`ruby --version`

_hit enter_

It should report you now using 2.3.1

Scenario: You are all set to run huginn but when you run it you get a callback trace error -- something along the lines of this:

Short snippet:

> 20:25:33 web.1 | [2016-07-12 17:25:33] INFO ruby 2.3.1 (2016-04-26) [x86_64-linux]

> 20:25:33 web.1 | [2016-07-12 17:25:33] INFO WEBrick::HTTPServer#start: pid=7027 port=3000

> 20:25:33 jobs.1 | /home/<your_username>/huginn/app/models/agents/twitter_stream_agent.rb:135:in `map': undefined method `strip' for {"filter1"=>["passwords", "leaked"]}:ActiveSupport::HashWithIndifferentAccess (NoMethodError)

> 20:25:33 jobs.1 | from /home/<your_username>/huginn/app/models/agents/twitter_stream_agent.rb:135:in `block in setup_worker'

> 20:25:33 jobs.1 | from /home/<your_username>/huginn/app/models/agents/twitter_stream_agent.rb:128:in `each'

> 20:25:33 jobs.1 | from /home/<your_username>/huginn/app/models/agents/twitter_stream_agent.rb:128:in `map'

> 20:25:33 jobs.1 | from /home/<your_username>/huginn/app/models/agents/twitter_stream_agent.rb:128:in `setup_worker'

> 20:25:33 jobs.1 | from /home/<your_username>/huginn/lib/agent_runner.rb:94:in `block (2 levels) in load_workers'

> 20:25:33 jobs.1 | from /home/<your_username>/huginn/lib/agent_runner.rb:62:in `block in with_connection'

leaving you back at the bash prompt.

Investigation: First, don't panic!

Scroll up to where you typed in the command to start huginn (bundle exec foreman start) and look just after that line. Somewhere (don't know how many lines down from it) you may see some kind of error. You should see something that definitely, when read into indicates some sort of problem. In this case, I've had this happen to me just fiddling around with specifying a Twitter agent filter. Obviously, my filter is messed up and it looks like the parsing of the filter is crashing huginn (bug?) and you wouldn't be expected to figure that out, but this line:

> home/<your_username>/huginn/app/models/agents/twitter_stream_agent.rb:135:in `map': undefined method `strip' for {"filter1"=>["passwords", "leaked"]}:ActiveSupport::HashWithIndifferentAccess (NoMethodError)

should definitely clue you in that something is seriously wrong with the password filter. Look again at the line, you also see the error is occurring in twitter_stream_agent. It's a likely bet you have a Twitter Stream Agent that is using the mentioned filter. No it's not a problem with the code (though perhaps the code should skip agents that have bad filters?). It's having a hard time dealing with what is likely an agent you created that has a malformed filter. So what? How do we deal with this? Well, the way I dealt with it, and it may not be suitable for you is to wipe out that particular agent. (REAL glad I decided to use separate Twitter Stream Agents for different sets of content searches -- otherwise one bad line would force me to wipe out the whole thing).

Solution 1) Wipe out that particular agent from your MySQL (MariaDB) table. Let's do this now.

While it may be easier and MUCH more tempting to use the MySQL Workbench or other utility; I'm going to force you to use the command line by not walking through a GUI-based DB manager. Yes it's more painful, but there's no substitution for learning at least the basic SQL commands. Not only is knowing SQL useful and a great skill to improve upon, it's also an incredible valuable skillset! Again, this is only the bare basics.

Drop to a terminal window if you're not already there.

Make sure MySQL is already started, you can do this by entering the following:

`ps aux | grep mysql`

_hit enter_

If it's already running, you should see something like (not EXACTLY, but LIKE) this:

> mysql 1913 0.0 5.7 705732 118752 ? Ssl 20:02 0:02 /usr/sbin/mysqld --defaults-file=/etc/my.cnf --user=mysql

If you see this, continue on. If not, enter the following:

`sudo service mysql start`

_hit enter_

(if prompted, enter your root password and hit enter)

now type:

`sudo mysql --socket=/var/run/mysql/mysql.sock -u root -p`

_hit enter_

_type in the database's root password_

_hit enter_

Now, at the MySQL shell

If you don't remember the names of your agents, you can enter:

`SELECT * FROM <_database_table_> WHERE type=<_agent type_>;`

So, FOR ME, the entire line was:

`SELECT * FROM huginn_development WHERE type="Agents::TwitterStreamAgent";`

From what I've seen it looks as though all types start with "Agents::"

Next enter:

`SELECT * FROM <_database_table_> WHERE name=<_name_of_the_bad_agent_>;`

_hit enter_

You're telling the databasing engine (MySQL/MariaDB) to present you a handle to all (the \* in the SELECT statement) records in the particular database table where the name field is equal to what you tell it.

replace <database_table> with the table the agent is sitting in; for me it was huginn_development.agents

replace <name_of_the_bad_agent> with the name of the agent that is causing the crash. For me I saw the filter listed in the crash when huginn started and saw it stated password and leak. This is part of my Twitter Stream Agent - password.

So, to recap, FOR ME the entire command was:

`SELECT * FROM huginn_development.agents WHERE name="Twitter Stream Agent - password";`

You should see it say something like:

> 1 row in set (0.00 sec)

Next enter (type **VERY** carefully the next line and double check the entry!):

`DELETE FROM <database_table> WHERE name=<name_of_the_bad_agent>;`

_hit enter_

You should see something like:

> Query OK, 1 row affected (<some time here...>)

So, FOR ME, it would've been:

`DELETE FROM huginn_development.agents WHERE name="Twitter Stream Agent - password";`

Next, you want to flush the changes so the modifications get made to the table

Do this by entering the following:

`FLUSH TABLES <_database_table_>;`

_hit enter_

If nothing has the database open, you should see:

> Query OK, 0 rows affected (0.00 sec)

now enter:

`quit`

_hit enter_

Solution 2) Surgically replace or null out the filter field. (Coming soon? -- Trying not to burn myself out)

Next try restarting huginn and it should start.
