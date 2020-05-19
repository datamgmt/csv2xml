# csv2xml
A Perl utility to convery an XML document into (multiple) csv files

## Name

xml2csv.pl 

## Synopsis

A utility to extract data from an XML file and put that data into csv files for reading into Excel or loading into a database.

The utility will also (optionally) do the following:

 * Create the DDL for the database
 * Create the scripts to load the data from the csv file to the database
 * Create a diagram of the tables and their relationships

## Description

This utility converts an XML file into a series of csv files. It also creates the a series of 'drop table' and 'create table' statements to load data into a database. As XML is a tree structured document the csv files and database tables created reflect the structure of the of the XML document. For simple documents the format is pretty intuitive, complex documents may take a little more to fully understand, however the output fully retains all the data in it's original structure.


## See Also

### For Users

 * [Getting Started](documentation/GettingStarted.md)
 * [Command Line Options](documentation/Options.md)
 * [Examples](documentation/Examples.md)

### For Developers
 
 * [Development Environment](documentation/DevelopmentEnv.md)
 * [Algorithm](documentation/Algorithm.md)
 * [Development Roadmap](documentation/Roadmap.md)
