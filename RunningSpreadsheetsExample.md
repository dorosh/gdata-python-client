# Introduction #

These instructions will guide you through running the example script which illustrates performing common operations using the spreadsheets modules.

# Details #

## Execution Environment ##

Make sure that the required modules are in your Python Path. See DependancyModules for a list of things you may need to install.

## Running the example ##

You can run the example from the main project directory by executing `python samples/spreadsheets/spreadsheetExample.py --user` _your user name_ `--pw` _your password_

You will be presented with a series of menus and you select the desired option by typing in a short line of text and pressing enter.

Once you have selected the spreadsheet and worksheet you would like to work with, you must choose which type of feed you will be working with, the cells feed, or the list feed.

To see all of the data in the selected worksheet, enter the command `dump` and the example application will print out the contents of each row (in the list feed) or each cell (in the cells feed).

You may exit the application at any time by terminating the application using control-D or control-C.