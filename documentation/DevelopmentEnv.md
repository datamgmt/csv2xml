# Development Environment

This page documents the tools that I use to develop the software in case you find it useful
It also gives credit to those who have developed the code on which I rely to do this work

* OS: macOS Catalina
* Editor: [Textmate](https://macromates.com/)
* Source Code Control System: [Github](https://github.com/) 
* SCCS Interface: [GitHub Desktop](https://desktop.github.com/)
* Perl Language: [ActivePerl](https://www.activestate.com/products/perl/downloads/)
* Perl Libraries: [CPAN](https://www.cpan.org/)
* Terminal Programme: [Emtec Zoc](https://www.emtec.com/zoc/)
* Diagraming: [Graphviz](https://www.graphviz.org/)

## Standards

Whereever possible I try to ensure that the code follows: 


> **[Perl Best Practices](http://shop.oreilly.com/product/9780596001735.do)**
> **Standards and Styles for Developing Maintainable Code**
> **By Damian Conway**

This doesn't make my coding good, but it does ensure that my poor programming is done in a consistent way!

In practice this means that a committed release should pass the following test with no errors:
```
perlcritic --brutal xml2csv.pl
```
returns
```
xml2csv.pl source OK
```
## CPAN Libraries 

The following CPAN libraries are used

   * Modern::Perl
   * Data::Dumper
   * English
   * File::Path
   * File::stat
   * Getopt::Long
   * List::Util
   * List::MoreUtils
   * Path::Class
   * Readonly
   * Scalar::Util
   * Text::CSV
   * utf8::all
   * XML::Simple
   * YAML::XS
   * Text::Template
   * IPC::Open3
   
   These can be automatically installed with:
```
sudo update_cpan
```