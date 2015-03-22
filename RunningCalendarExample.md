# Introduction #

These instructions will guide you through running the example script which illustrates performing common operations using the calendar modules.

# Details #

## Execution Environment ##

Make sure that the required modules are in your Python Path. See DependencyModules for a list of things you may need to install.

## Running the example ##

You can run the example from the main project directory by executing `python samples/calendar/calendarExample.py --user` _your user name_ `--pw` _your password_  `--delete` _(true|false)_

The example will run through a series of actions including printing the list of calendars, retrieving all events from the primary calendar of the authenticated user, querying for events based upon a full text query and a date range query, inserting a single occurrence and a recurring event, updating an event to change the title, adding an extended property to an event, adding a reminder to an event, and, optionally, cleaning up by deleting the created events.

Please see the docstrings within the code for more information about each action.

This example should get you started developing applications using the Google Calendar data API very quickly.

If you have any problems running this example, or any other questions about the Calendar data API, please visit the [developer forum](http://groups.google.com/group/google-calendar-help-dataapi)