# Examples

The code comes with a series of example XML outputs and a utility to test your own XML files to see what the output is likely to look like.

## Running the examples

Once xml2csl.pl is set up as per the instructions simply type:

```
run_examples
```

## Examples directory Structure

```
\                                  # Root of the whole git project
\bin                               # Directory where xml2csv.pl and run_examples live
\examples                          # Root of the directory structure
\examples\configs                  # The configuration files to be used to generate the examples
\examples\output                   # The root of where the output from running the examples will be stored
\examples\output{xmlfile}\{config} # Output from running xml2csv.pl on {xmlfile} using {config} configuration
\examples\templates                # The template files to be used to generate the examples
\examples\xml                      # The xml files to be used to generate the examples

```

## Adding your own XML files

If you want to see how your own XML files will look simply put them in the examples\xml directory and re-run run_examples to generate the required output
Note: You are advised to put small sample files here to experiment as this utulity generates many different versions of the output and will take time to run


## Trying your own config settings

If you want to try your own combination of configurations simply put a new config file in the examples\configs directory and re-run run_examples to generate the required output

