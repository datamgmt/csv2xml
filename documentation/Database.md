# Database and output formatting support

Unfortunately database systax varies and so it is not possible to create a single script that will work on all databases.

In order to allow support for multiple databases the Perl module [Text::Template](https://metacpan.org/pod/Text::Template) is used.

This allow a number of different database syntaxes to be stored in the YAML file [templates/database.yaml](templates/database.yaml)

The distributed database.yaml file contains support for

* CSV with a header record (csv_header)
* CSV without a header record (csv_noheader)
* Oracle (oracle)
* MySQL (mysql)
* Postgres (postgres) - this is the default

But other databases can easily be added

## How the default Postgres entry is built

Here are the postgres lines from the YAML file for one type of database (postgres). The file can have as many entries as you want, 

```
postgres:
  create: |-
    /*
    {$comments}
    */

    CREATE TABLE {$table} (
    {$columns});
  csv: |-
    {$header}
    {$records}
  drop: |-
    /*
    {$comments}
    */

    DROP TABLE IF EXISTS {$table};
  integer: INTEGER
  load: |-
    /*
    {$comments}
    */

    \COPY {$table} FROM '{$datafile}' DELIMITER '{$delimiter}' CSV HEADER;
  numeric: NUMERIC
  run: |-
    \I {$script}
  runscript: run_all_scripts.sql
  pelt: |-
    command:postgres_alias:{$script}:
  peltscript: run_all_scripts.idx
  varchar: VARCHAR
```

## The elements of the entry

An entry can have up to 12 elements depending on the required output. Those elements are:

These elements define the keywords used by the database

 * integer - the key word used for an integer - sometimes INT, or INTEGER, etc
 * numeric - the key word used for a numeric - somtimes NUMBER, NUMERIC, FLOAT, etc
 * varchar - the key word used for a string - simetimes VARCHAR, VARChAR2 (Oracle), TEXT, etc.

 If any of these are defined then a file of the relevent type will be created using the syntax described
 
 * csv - the syntax for a csv file
 * create - the syntax for a create table statement in a script
 * drop - the syntax for a drop table statement in a script
 * load - the syntax for a load file statement in a script
 * loadext - the extension of the load script - defaults to 'sql' but Oracle requires 'ctl' for SQL Loader

If there is a a script file defined then it will create a script file to run all the other scripts

 * run - the syntax to run another script
 * runscript - the name of the script used to run all the other scripts
 * pelt - the syntax to run scripts using the datamgmt.com PELT tool
 * peltscript - the name of the script used to run the PELT job

Note: pelt lines can be omitted if you do not have access/use PELT

## The Substitution variables

Substitution variables are of the format `{$variable}`. When a string of the required format is parsed it is replaced with the value of that variable

The defined variables are:

 * $header - the delimited list of field names using the defined delimited
 * $records - all of the individually parsed records joined togther for the csv file
 * $table - the table name in thr create and/or drop scripts
 * $columns - all of the column names used in the create table statement
 * $datafile - the name of the csv data file
 * $delimiter - the deimiter between fields - usually comma (,)
 * $script - the name of the script created to create, drop or load a table
 * $comments - omment fields describing where and how the file has been generated
 
## Creating/Modifying your own

Hopefully there is enough infomation to understand the process above.

The easiest way to create your own template is to cut and paste all of the postgres section then change its name to whatever you want.
Now go through each section and make the changes you require. Run the xml2csv.pl on a test xml file and examine the output. Some trial and error will soon produce the output you want.

Note: if you mis-configure the template the xml2csv script can blow up quite dramatically - if this happens check the template first and revert your changes and try again.