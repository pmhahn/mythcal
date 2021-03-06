# mythcal

Copyright 2009-2014 Richard Fearn

## Introduction

mythcal is a simple script that synchronizes your MythTV recording schedule to
a Google calendar.

Leaving my MythTV server on 24/7 wastes electricity, but I don't want to forget
to turn it on to record programmes. I wrote this to make it easy to keep track
of upcoming recordings.

## Getting started

1. Create a calendar in Google Calendar that will hold your MythTV programmes.
   DO NOT USE YOUR MAIN GOOGLE CALENDAR! YOU MUST CREATE A NEW CALENDAR!
   mythcal synchronises your programmes by deleting everything from the
   calendar, then adding an event for each programme.

2. Create a new directory somewhere on your MythTV server and copy the script
   (`mythcal`) and the template configuration file (`mythcal.conf.template`) into
   the directory.

3. Install the required packages:

    * MythTV Python bindings (`"libmyth-python"` for Ubuntu; `"python-MythTV"`
      from RPM Fusion free for Fedora).

    * pytz (`"python-tz"` for Debian and Ubuntu; `"pytz"` for Fedora).

    * Google APIs Client Library for Python (`"python-googleapi"` for Ubuntu).

4. Copy the template configuration file, `mythcal.conf.template`, to
   `mythcal.conf`, and add the missing settings. The sections are:

    * `[mythtv]` - details about your MythTV server. `"timezone"` should be a
      zoneinfo time zone name such as `"Europe/London"`. To find an appropriate
      time zone name, use the supplied `timezones` script (see below).

    * `[calendar]` - details about your Google Calendar. To find the `"id"`, go into
      Google Calendar Settings, open the "Calendars" tab, click the calendar you
      want to use, and look in the "Calendar Address" section. The Calendar ID
      should be displayed: it will look something like
      `"abc123def@group.calendar.google.com"`. Please remember: USE A SEPARATE
      CALENDAR FOR MYTHCAL, or your appointments will be deleted!

5. Give mythcal permission to access your calendar. Run `mythcal --auth` and
   follow the instructions.

6. Run mythcal manually with the `--dry-run` or `-n` option. This will tell you
   what's going to be changed in your Google Calendar. Hopefully it won't tell
   you that your important appointments are going to be deleted, because you'll
   be using a **separate** calendar for mythcal!

7. If everything looks good, set up a cron job which will execute mythcal as
   often as you like. The command being run should look something like this:

   `cd /path/to/mythcal/directory && ./mythcal`

## Finding an appropriate time zone name

The `timezones` script can be used to find an appropriate time zone name.
Running it with no parameters lists all time zone names. If a parameter is
given, the script does a case-insensitive search for time zones containing
that text. For example:

    $ ./timezones york
    America/New_York

## Acknowledgements

Thanks to Michael T. Dean and Raymond Wagner for pointing me in the direction
of the MythTV Python bindings.

## Useful documentation

[Google Calendar APIs and Tools - Data API Developer's Guide: Python](http://code.google.com/apis/calendar/data/1.0/developers_guide_python.html)

[Google Data Protocol - Batch Processing in the Google Data Protocol](http://code.google.com/apis/gdata/docs/batch.html)
