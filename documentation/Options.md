# Command Line Options & Configuration Files

xml2csv.pl has multiple options as can be seen below. The optionion names can be shortened as long as they remain unqiue so --c, --ca, --cas and --case are all identical. Also the program will accept -- (minus,minus), - (minus) or + (plus) as a parameter. Boolean options are negated by prefixing the command with 'no' so , for example '--noremove_crlf' will not remove 'cr/lf' from data whilst --remove_crlf will remove 'cr/lf' for data

These parameters (all with the same names) can be set in the configutation file (default name config.yaml). Where items are boolean they are set to either 1 (TRUE) or 0 (FALSE)  rather than prefixing with (no)

Each of the commands is described below:

## xml2csv.pl --help

The help command displays a list of all the available options:

```
Usage: xml2csv.pl [options]

Options:
       --(no)allow_file_overwrite    default=allow_file_overwrite
       --(no)allow_surrogate_ids     default=allow_surrogate_ids
       --case=string                 default='lower'
       --diagram_template=string     default='monochrome'
       --diagram_type=string         default='all'
       --graphviz_command=string     default='dot -Tpdf -O '
       --help
       --indent=integer              default=3
       --interval=integer            default heuristically defined
       --(no)list_templates          default=nolist_templates
       --load_config_file=string     default='config/config.yaml'
       --load_diagrams_file          default='config/diagrams.yaml'
       --load_structure_file=string  default=''
       --load_template_file=string   default='config/database.yaml'
       --load_xml_file=string        default='data.xml'
       --quiet                     
       --(no)remove_crlf=boolean     default=noremove_crlf
       --sample_size=integer         default=10
       --save_config_file=string     default='saved_config.yaml'
       --save_counts_file=string     default='saved_counts.txt'
       --save_diagram_file=string    default='diagram.dot'
       --save_path=string            default='output'
       --save_structure_file=string  default='saved_structure.yaml'
       --substitution_string=string  default='_x2c'
       --template=string             default='postgres'
       --usage                 
       --verbose                     
       --(no)CSV_always_quote        default=noCSV_always_quote
       --CSV_escape_char=char        default='"'
       --CSV_quote_char=char         default='"'
       --CSV_sep_char=char           default=','
       --XML_ContentKey=string       default='-content'
       --(no)XML_ForceArray          default=XML_ForceArray 
       --(no)XML_ForceContent        default=XML_ForceContent
       --(no)XML_KeepRoot            default=XML_KeepRoot
       --(no)XML_NoAttr              default=noXML_NoAttr
       --(no)XML_NormaliseSpace      default=noXML_NormaliseSpace
       --(no)XML_SuppressEmpty       default=1

For further information see: https://github.com/datamgmt/xml2csv
For further information on CSV_ options see: https://metacpan.org/pod/Text::CSV
For further information on XML_ options see: https://metacpan.org/pod/XML::Simple
```

## --(no)allow_file_overwrite
 
default=allow_file_overwrite

By default xml2csv.pl will just overwrite files. By setting this to noallow_file_overwrite the output directory must either not exist (in which case it is created at run time) or must be emply in order for the program to run
 
## --(no)allow_surrogate_ids
 
default=allow_surrogate_ids
 
 By default the programme will create a number of surrogate keys in the database in order to keep track of relationships between elements. If you do not require the surrogate keys then noallow_surrogate_ids turns them off. By default a surrogate key will have a suffix of _x2c_id to make it easily recognisable and prevent name clashes with existing data fields. This can be changes with --substitution_string (see below)
 
 See examples: noallow_surrogate_ids
 
## --case=string                 
 
default='lower'

Defines whether column names are convertedto one case or another. 'lower', the default, converts them all to lowercase; 'upper' converts them all to uppercase and 'mixed' leaves them as found in the xml file used as a source.

See examples: case_lower, case_upper, case_mixed
 
## --diagram_template=string     
 
default='monochrome'

The layout for diagrams is determined by a temp,ate found in config/diagrams.yaml. By default the programme comes with two templates 'monochrome' and 'colorful'. You can either modify these templates or create new ones to suit your needs [Diagrams](configuration/Diagrams.md) for information on creating/modifying templates and --list_templates to get a list of all currently available templates.

See examples:  diagram_template_colorful

## --diagram_type=string         
 
default='all'

A diagram will always contain the table name, however it may also contain the columns of the table or a sample data set. The valid values are: 'none' which switches off diagram creation; 'basic' which returns just the table name;  'model' which returns the table anme and column details; 'sample' which returns the table name and a sample of the data; 'all', the default, which returns the table name, column name, and sample data.

See examples: diagram_type_none, diagram_type_basic, diagram_type_model, diagram_type_sample

## --graphviz_command=string     
 
default='dot -Tpdf -O '

This is the command required to create a diagram using Graphviz. By defaul it assumes that the 'dot' command is available in your path and that you want a PDF output. Further information can be found at [Graphviz Command Line Invocation](https://graphviz.gitlab.io/_pages/doc/info/command.html)
 
## --indent=integer              

default=3

This command determines the inent level of SQL statements that are generated. By default this is set to 3 but can be set to any integer

See example: indent

## --interval=integer            

default heuristically defined

This command determines how frequently a progress message is printed out at verbose level 4 or greater. It is calculated from the size of the file automatically with larger files having less frequent updates however it can be set from the command line if you have a particular need.

## --(no)list_templates          

default=nolist_templates

Lists the available database and diagram templates' For a default configuration this will return the following

```
Available templates:

The load_template_file called config/database.yaml contains:

   csv_header
   csv_noheader
   mysql
   oracle
   postgres

The load_diagrams_file called config/diagrams.yaml contains:

   colorful
   monochrome
```

## --load_config_file=string     

default='config/config.yaml'

This file contains the settings for the program. This option allows the system to use alternative config files specified either by an absolute or relative path. Files are in YAML format.

## --load_diagram_file=string

default='config/diagrams.yaml'

This file contains information on how to lay out the diagrams. This option allows the system to use alternative diagram files specified either by an absolute or relative path. Files are in YAML format. For further information on creating and editing these files see [Diagrams](documentation/Diagrams.md)

## --load_structure_file=string  

default=''

This file contains information on the data structure. This option allows the system to import an exisitng data structure specified either by an absolute or relative path. Files are in YAML format. For further information on creating and editing these files see [Structure](documentation/Structure.md)

## --load_template_file=string   

default='database.yaml'

This file contains database specific syntax information. This option allows the system to use alternative database files specified either by an absolute or relative path. Files are in YAML format. For further information on editing these files see [Database](documentation/Database.md)

## --load_xml_file=string        

default='data.xml'

This is the XML file you want to process. This option allows tthe user to specify a file to read in either by an absolute or relative path.

## --quiet                     

This option decrements the verbose-ness of the messages by 1 for each occurence - the default is 3 so 'xml2csv.pl -q -q -q' will reduce the verbose level to 0. It is the opposite of --verbose (which increments by 1) 

## --(no)remove_crlf=boolean     

default=noremove_crlf

By default data it left unmodified in the output csv however sometimes it is desirable to remove carriage returns and line feeds in which case the --remove_crlf option does this. The programme uses the Perl '\R' operator to identify generic newlines - for further information on it's behaviour see [Perldoc](https://perldoc.perl.org/perlrebackslash.html#Misc).

See example: remove_crlf

## --sample_size=integer         

default=10

The diagram types 'sample' and 'all' will include a sample of the data from the XML file. By default it will return the first 10 rows or all rows if less than 10 exist. This option can be used to increase or decrease the sample size however it should be noted that very large samples may be undesirable becuase of the time to generate or the possibility of running out of memory whilst running the programme.

See exmaple: sample_size

## --save_config_file=string     

default='saved_config.yaml'

This option means that the system will create a file with the name passed in the output directory that contains the entire configuration as run. This is useful in circumstances where you want to re-run a load (e.g. a daily load) and always want to use the same configuration.The saved file can be used with the --load_config_file option. An empty string means that no file will be written.

## --save_counts_file=string     

default='saved_counts.txt'

This option writes a file of the named parameter that contains the name of each record and the number of records found for each table. This is useful for audit purposes. An empty string means that no file will be written

## --save_diagram_file=string    

default='diagram.dot'

This option means that the system will create a file with the name passed in the output directory that contains the giagram in Graphviz 'dot' format. The type of diagram used is determinined by the --diagram_template option. An empty string means that no file will be written, which is equivalent to --diagram-type=none

## --save_path=string            

default='output'

This is the name of the directory where all the output will be saved. If the directory does not exist it will be created. The directory can be an absolute or relative path.

## --save_structure_file=string  

default='saved_structure.yaml'

This option means that the system will create a file with the name passed in the output directory that contains the structure configuration that was found in the input xml file. This is useful in circumstances where you want to re-run a load (e.g. a daily load) and ensure certain fieds are included even though they may not appear in some input files. The saved file can be used with the --load_structure_file option. An empty string means that no file will be written. For further information on using and editing these files see [Structure](documentation/Structure.md)

## --substitution_string=string  

default='_x2c'

For the generation of surrogate keys and in cirtain other conditions a unique string is required to identfy data generated by xml2csv.pl. The default is to use _x2c which is probably pretty unique but can be varied if required.

See example: substitution_string

## --template=string             

default='postgres'

This option determines the format of the scripts generated by the utility. This is useful if you want to load the output into a SQL database. By default it generates 'postgres' scripts, but can also generate mysql and oracle database scripts. In addition there are options for csv only with a header record (csv_header)  and csv only with no header record (csv_noheader). This file can be modified to vary the output as required and add new output formats. The currently available templates can be viewed with --list_templates. For further information on editing these files see [Database](documentation/Database.md)

See examples: template_csv_header, template_csv_no_header, template_oracle, template_mysql
## --usage                 

A synonym for --help

## --verbose                     

This option increments the verbose-ness of the messages by 1 for each occurence - the default is 3 so 'xml2csv.pl -v -v' will increase the verbose level to 5. It is the opposite of --quiet (which decrements by 1) 

## --(no)CSV_always_quote        

default=noCSV_always_quote

This encapsulates all data with the configured quote character.

The programme uses the Perl module Text::CSV to format the CSV record and file. This option can be passed directly through to the module. For further information see [always_quote](https://metacpan.org/pod/Text::CSV#always_quote)

See example: CSV_always_quote

## --CSV_escape_char=char        

default='"'

This changes the escaping character from the default of double quotes (")

The programme uses the Perl module Text::CSV to format the CSV record and file. This option can be passed directly through to the module. For further information see [escape_char](https://metacpan.org/pod/Text::CSV#escape_char)

See example: CSV_escape_char

## --CSV_quote_char=char         

default='"'

This changes the quoting character from the default of double quotes (")

The programme uses the Perl module Text::CSV to format the CSV record and file. This option can be passed directly through to the module. For further information see [quote_char](https://metacpan.org/pod/Text::CSV#quote_char)

See example: CSV_quote_char

## --CSV_sep_char=char           

default=','

This changes the seperating character from the default of comma (,)

The programme uses the Perl module Text::CSV to format the CSV record and file. This option can be passed directly through to the module. For further information see [sep_char](https://metacpan.org/pod/Text::CSV#sep_char)

See example: CSV_sep_char

## --XML_ContentKey=string       

default='-content'

The default is usually sufficient

The programme uses the Perl module XML::Simple to read the XML file. This option can be passed directly through to the module. For further information see [ContentKey](https://metacpan.org/pod/XML::Simple#ContentKey-=%3E-'keyname'-%23-in+out-seldom-used)

See example: XML_ContentKey

## --(no)XML_ForceArray          

default=XML_ForceArray 

This is an important attribute for influencing how your XML data is ultimately structured in the CSV

This option should be set to '1' to force nested elements to be represented as arrays even when there is only one. Eg, with ForceArray enabled, this XML:

```
<opt>
  <name>value</name>
</opt>
```

would parse to this:

```
{
  'name' => [
              'value'
            ]
}
```

instead of this (the default):

```
{
  'name' => 'value'
}
```


The programme uses the Perl module XML::Simple to read the XML file. This option can be passed directly through to the module. For further information see [ForceArray](https://metacpan.org/pod/XML::Simple#ForceArray-=%3E-%5B-names-%5D-%23-in-important)

See example: XML_ForceArray 

## --(no)XML_ForceContent        

default=XML_ForceContent

This is an important attribute for influencing how your XML data is ultimately structured in the CSV

When XMLin() parses elements which have text content as well as attributes, the text content must be represented as a hash value rather than a simple scalar. This option allows you to force text content to always parse to a hash value even when there are no attributes. So for example:

```
XMLin('<opt><x>text1</x><y a="2">text2</y></opt>', ForceContent => 1)
```

will parse to:

```
{
  'x' => {           'content' => 'text1' },
  'y' => { 'a' => 2, 'content' => 'text2' }
}
```

instead of:

```
{
  'x' => 'text1',
  'y' => { 'a' => 2, 'content' => 'text2' }
}
```

The programme uses the Perl module XML::Simple to read the XML file. This option can be passed directly through to the module. For further information see [ForceContent](https://metacpan.org/pod/XML::Simple#ForceContent-=%3E-1-%23-in-seldom-used)

See example: XML_ForceContent

## --(no)XML_KeepRoot            

default=XML_KeepRoot

This is an important attribute for influencing how your XML data is ultimately structured in the CSV

In its attempt to return a data structure free of superfluous detail and unnecessary levels of indirection, XMLin() normally discards the root element name. Setting the 'KeepRoot' option to '1' will cause the root element name to be retained. 

The programme uses the Perl module XML::Simple to read the XML file. This option can be passed directly through to the module. For further information see [KeepRoot](https://metacpan.org/pod/XML::Simple#KeepRoot-=%3E-1-%23-in+out-handy)

See example: XML_KeepRoot 

## --(no)XML_NoAttr              

default=noXML_NoAttr

This is an important attribute for influencing how your XML data is ultimately structured in the CSV

When used with XMLout(), the generated XML will contain no attributes. All hash key/values will be represented as nested elements instead.

When used with XMLin(), any attributes in the XML will be ignored.

The programme uses the Perl module XML::Simple to read the XML file. This option can be passed directly through to the module. For further information see [NoAttr](https://metacpan.org/pod/XML::Simple#NoAttr-=%3E-1-%23-in+out-handy)

See example: XML_NoAttr     

## --(no)XML_NormaliseSpace      

default=noXML_NormaliseSpace

The default is usually sufficient

This option controls how whitespace in text content is handled. Recognised values for the option are:

 * 0 = (default) whitespace is passed through unaltered (except of course for the normalisation of whitespace in attribute values which is mandated by the XML recommendation)
 * 1 = whitespace is normalised in any value used as a hash key (normalising means removing leading and trailing whitespace and collapsing sequences of whitespace characters to a single space)


The programme uses the Perl module XML::Simple to read the XML file. This option can be passed directly through to the module. For further information see [NormaliseSpace](https://metacpan.org/pod/XML::Simple#NormaliseSpace-=%3E-0-%7C-1-%7C-2-%23-in-handy)

See example: XML_NormaliseSpace  

## -XML_SuppressEmpty       

default=1

This option controls what XMLin() should do with empty elements (no attributes and no content). The default behaviour is to represent them as empty hashes. Setting this option to a true value (eg: 1) will cause empty elements to be skipped altogether. 

The programme uses the Perl module XML::Simple to read the XML file. This option can be passed directly through to the module. For further information see [SuppressEmpty](https://metacpan.org/pod/XML::Simple#SuppressEmpty-=%3E-1-%7C-''-%7C-undef-%23-in+out-handy)

See example: XML_SuppressEmpty  

