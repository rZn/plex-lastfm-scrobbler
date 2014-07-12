plex-lastfm-scrobbler
=====================

plex-lastfm-scrobbler provides a set of scripts that allow you to scrobble played audio items to Last.FM from the Plex Media Server application. plex-lastfm-scrobbler was built to run across platforms, while it has not yet been tested on Windows, it *should* work. 

A few points

  - Uses python standard library. Python is the only requirement to run this application
  - Must be run on the Plex Media Server 
  - Parses Plex Media Server logs for the 'got played' string in the log file.
  - Does not differentiate between clients. Meaning all media played, will be scrobbled while the script is running.


Installation
----

Version 0.0.1

It is recommended (but not required) that you install this into a virtualenvironment. 

```
virtualenv ~/.virtualenvs/plex-lastfm-scrobber
source ~/.virtualenvs/plex-lastfm-scrobber/bin/activate
```

Fetch and install the source from the github repo.
```
git clone git@github.com:jesseward/plex-lastfm-scrobbler.git
cd plex-lastfm-scrobbler
python setup.py install

```

You're done.


Configuration
-----------

The plex-lastfm-scrobbler configuration file (plex_scrobble.conf) is installed to ~/.config/plex-lastfm-scrobbler/ . The following configuration values are available.

If you're running Plex Media Server on a Linux based operating system, things should work out of the box.

```
# REQUIRED: mediaserver_url is the location of the http service exposed by Plex Media Server
# the default values should be 'ok', assuming you're running the plex scrobble
# script from the same server as your plex media server
mediaserver_url = 'http://localhost:32400'

# REQUIRED: mediaserver_log_location references the log file location of the plex media server
# the default under /var/lib/... is the default install of plex media server on 
# a Linux system. You may wish to change this value to reference your OS install.
mediaserver_log_location = '/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Logs/Plex Media Server.log'

# REQUIRED: Where do you wish to write the plex-scrobble log file.
log_file = /tmp/plex_scrobble.log

```

Running
--------

If you installed plex-lastfm-scrobble to a virtual environment, enable the virtual env.

```
source ~/.virtualenvs/plex-lastfm-scrobber/bin/activate
```

run the application
```
$ plex-scrobble.py
```
On first run you will be prompted to authenticate and grant access to your Last.fm account. Visit the URL generated by plex-scrobble and follow the prompts to grant access to the application.

Example.


```
$ plex-scrobble.py

== Requesting last.fm auth ==
Please accept authorization at http://www.last.fm/api/auth/?api_key=blunted_dummies-house-for-all-1991

Have you authorized me [y/N] : y
Please relaunch plex-scrobble service.

```

Once this is complete, please re-start the service, listen to audio via Plex and watch as your music is scrobbled. You may wish to leave the service running in the background. On a POSIX system, wrap the script in the no-hangup utility.

```
$ nohup plex-scrobble.py &
```

Troubleshooting
-------------

* If you're experiencing authentication issues (appearing in plex_scrobble.log), remove the ~/.config/plex-lastfm-scrobbler/session file. This stores your Last.FM authentication token. There is no harm in removing/recreating this as many times as needed. 
* Log an issue https://github.com/jesseward/plex-lastfm-scrobbler/issues/new

Contributing 
-----------
Any feedback on the performance on a MS Windows installation would be appreciated. I do not have ability to test plex-lastfm-scrobbler on this platform. Please log an issue or a pull request with any fixes.


