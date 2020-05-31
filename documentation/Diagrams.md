# Diagrams and output formatting support

xml2csv.pl exploits graphviz to generate diagrams in png or pdf format

In order to allow support for multiple databases the Perl module [Text::Template](https://metacpan.org/pod/Text::Template) is used.

This allow a number of different diagram formats to be stored in the YAML file [templates/diagrams.yaml](templates/diagrams.yaml)

The distributed diagrams.yaml file contains support for

* monochrome - a black and white layout
* colourful -a colourful layout

But other diagrams can easily be added

## How the default Monochrome entry is built

Here are the monochrome lines from the YAML file, you can have as many entries as you want, 

```
monochrome: 
  columnname_record: |1-
                   <tr>
                      <td align="left" border="0">{$column_name}</td>
                      <td align="left" border="0">{$column_type}</td>
                   </tr>
  columnname_table: |1-
   <table border="0">
                   <tr>
                      <td align="left" border="0" colspan="2"><b>Columns:</b></td>
                   </tr>
    {$columnname_records}
                </table>
  data_headers: |1-
               <tr>
   {$data_header}                </tr>
  data_header: |1
                      <td align="left" border="0" bgcolor="#d0d0d0">{$column_name}</td>
  data_record: |1
                   <tr>
   {$data_rows}                </tr>
  data_row: |1
                      <td align="left" border="0" bgcolor="#eeeeee">{$data_cell}</td>
  data_table: |1-
      <table border="0">
                   <tr>
                      <td align="left" border="0" colspan="2"><b>{$data_name}</b></td>
                   </tr>
       {$data_headers}
    {$data_records}             </table>
  graph: |1-
    digraph G \{
       rankdir=LR;
       node [shape=plaintext];
      
      {$tables}
   {$relationships}
    \}
  omitted_table: |-
      "{$table_id}" [label=<
         <table style="rounded, dashed">
            <tr>
               <td border="0" align="left">
                  <b>Omitted Table:</b> {$omitted_tablename}
               </td>
            </tr>
         </table>
      >];
  relationship: |1
   "{$parent_table_id}" -> "{$table_id}";
  surrogate: |1
   <i>{$surrogate}</i>
  table: |3
      "{$table_id}" [label=<
         <table style="rounded">
            <tr>
               <td border="0" align="left">
                  {$tablename_table}
               </td>
            </tr>
            <tr>
               <td border="0" align="left">
                  {$columnname_table}
               </td>
            </tr>
            <tr>
               <td border="0" align="left">
               {$data_table}
               </td>
            </tr>
         </table>
      >];
  tablename_table: |-
      <table border="0">
                   <tr border="0">
                      <td align="left" border="0"><b>Table:</b></td>
                      <td align="left" border="0">{$tablename}</td>
                   </tr>
                </table>

```

## The elements of the entry

An entry can have up to 12 elements depending on the required output. Those elements are:

*  columnname_record - the structure of a single column in the columns section
*  columnname_table - the structure of all the column information generated from the columnname_records
*  data_headers - the headers of the sample data section
*  data_header - the header for a single field in the sample data section
*  data_record - a single field iin the sample data section
*  data_row - a single row iin the sample data section
*  data_table - the structure of all the data information generated from the data_ records
*  graph - the entire graphviz graph structure
*  omitted_table - the structure required for omitted tables
*  relationship - the structure required to draw relationships
*  surrogate - the structure required for surrogate keys
*  table - the graphviz table structure 
*  tablename_table the structure for the information about the table

## The Substitution variables

 * $columnname_table - the table that holds all the column info
 * $column_name - the field that holds the column name in the columns table
 * $column_type - the field that holds the column type information in the columns table
 * $data_cell - the field that holds the sample data field
 * $data_header - the field that holds the sample data header field
 * $data_headers - the field that holds the combined sample data header fields
 * $data_name - the information about the sample
 * $data_records - all of the data records shown
 * $data_rows - all of the rowns in the data table
 * $data_table - the table with all the data in it
 * $omitted_tablename - the ommitted table from the XML formating
 * $parent_table_id - the parent table_id in a relationship_
 * $relationships - all of the relationships
 * $surrogate - the surrogate key fields
 * $tablename - the tablename in the tablename table
 * $tablename_table - the contents of the tablename table
 * $tables - the table that holds the sub-tables
 * $table_id - the internal id of the table - used as the node name

                                
## Creating/Modifying your own

Hopefully there is enough infomation to understand the process above.

The easiest way to create your own template is to cut and paste all of the monochrome section then change its name to whatever you want.
Now go through each section and make the changes you require. Run the xml2csv.pl on a test xml file and examine the output. Some trial and error will soon produce the output you want.

Note: if you mis-configure the template the xml2csv script can blow up quite dramatically - if this happens check the template first and revert your changes and try again.
