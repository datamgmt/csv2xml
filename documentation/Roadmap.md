# Development Roadmap

The following sections outline the ideas I have for future development and the priorities given to them.
There is no guarentee when or if these will ever be done.

If there are any features and/or issues please contact me here:

https://github.com/datamgmt/xml2csv/issues

Additional contributors are also welcome.

## Version 1 - Basic (Current Version)

    * Split structure and data writes
    * Test reserved/bad words functionality
    * Add key and copyright to diagram
    * Check inline TODOs
    * Add log to file
    * Add Message Numbers
    * Final tidy-up and perlcritic —brutal
    * Update docs and README.md
    * Create examples for documentation
    * TBD - Display Message caller code
    * TBD - Add debug options
    
## Version 2 - Profiling

    * Add data profiling option (potentially using List::MoreUtils) including:
    
        * Nulls
        * Max/Min
        * Discreet values
        
    * Add primary/foreign key generation 
    * Stop at xml level/depth n
    
## Version 3 - Large File Handling

    * Cache data by level 
    * Split XML and process in chunks
    
## Version 4 - Neo4j support

## Version 5 - Python version ?