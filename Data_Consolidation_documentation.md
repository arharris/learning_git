template for documentation
# Title
Examples: "Verasol Data Consolidation," "California Biomass Residue Emissions Characterization"
#### Version Number

## Purpose
Here's where you would briefly describe the overall intent of the software, with a very generalized discussion of input and output. 

## Quick Instructions
I don't know about you, but I loathe finding a recipe online and having to read someone's life story before they tell me the recipe. Unless it is absolutely critical to the understanding of how to use the software, there should be basic instructions here, near the start of the documentation, of how to use the software in question. This section should contain enough information to successfully use the program, and if there are any key details which may trip up the user, explain those as well.

## Detailed Instructions
If the software merits it, here's where we have a more detailed set of instructions on how the software functions and how to use it. If there are multiple functions or options, here's where they would be explained.

## Inputs
Detail the necessary inputs to run the software. This could be input files, variable parameters that must be entered, or some other input to the program. Input file structure should be explained.

## Outputs
Detail the expected output of the software, and if necessary, any additiuonal information needed to interpret or use these outputs.

## Common Torubleshooting
If common, relatively easy troubleshooting issues ahve been identified in the development and testing of code, detail that here. Depending on the software and the complexity involved, this may not be relevant for all software.

Documentation for Verasol
# Verasol Data Consolidation
#### Version 2.0

## Purpose
This suite of scripts is designed to take the individual product testing results and consolidate them as an Rdata object. This Rdata object can be used as a pseudo-database for broader analysis.

## Quick Instructions
### 1. Start up an R instance, and open up "consolidate_data_exports.R"  
Currently, script must be implemented in an R instance (RStudio is ideal, but if you are comfortable with the base R GUI, that works as well). If using the base R GUI, you will need to open up a text editor (such as VIM, BBEdit, or Notepad++) to access the .R file.

### 2. Check the hard-coded file paths
There are a few places where consolidate_data_exports.R relies hard-coded file paths to access key functions and data resources:
1. Immediately following the version notes at the start of the file, there is a section labeled "LOAD FUNCTIONS USED IN THIS SCRIPT". There are two lines issuing "source()" commands, with file paths pointing to "generic_functions.R" and "consolidate_data_exports_functions.R". 
2. In the next section, labeled "COMMAND LINE OPTIONS", the variables "main.dir" and "output.file.dir" point to the "All_Data_Exports" and "Verasol Data Analysis" directories, respectively. 
3. In the next section, labeled "CREATE A LABS LIST", the variable "labs.on.file" is pointed to file "labs.csv".

Make sure the file paths are relevant to your computer, and update them if necessary. NOTE: On computers running Windows, file paths are frequently shown with forward slashes ("\") as opposed to back slashes ("/"). In many programming languages, including R, forward slashes are used as an "escape character" (which tells the machine to ignore the next character) or in formatting (for example, "\n" means "start a new line"). So, be sure to use back slashes in your file paths.
