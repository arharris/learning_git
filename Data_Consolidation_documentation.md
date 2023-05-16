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
Detail the expected output of the software, and if necessary, any additional information needed to interpret or use these outputs.

## Common Troubleshooting
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

### 3. Run the code
If you are using the R GUI, you will need to copy and paste the code into the console and hit 'Enter'. In RStudio, you can either use the copy/paste method, or select all text in script, and hit the "Run" button at the top of the file window.

### 4. Check back periodically to make sure the script is running smoothly
Depending on how many new reports are in the data export directory, the script may take a while to fully run - you should see the names of data export directories printing to the console screen as the script progresses. Occasionally, the script will crash - sometimes because of a faulty data export, and sometimes because the machine just hates you. If this happens, don't panic - the script periodically saves progress, so not much has been lost. Find the most recently processed directory (this will be the last directory name printed to the screen), review the directory's data to check for errors (see the Troubleshooting guide), and then restart the script.

## Detailed Instructions
I don't think there is a need for more detailed instructions; the're currently not a lot of variation in how this script will be used. Keep as a template example ("Here's a script where detailed descriptions would not be used!") but delete from the readme.

## Inputs
The only inputs required for this software are the test report export files. Below is the expected directory structure for several products:
<pre>
├── All_Data_Exports
|   ├── PICO_SMQ_AR_ShenzhenSolarRunSR25Components_11132019
|   |   ├── BatteryExport
|   |   |   ├── ExportData.csv
|   |   ├── VisualScreeningExport
|   |   |   ├── BatteryInfo.csv
|   |   |   ├── BatteryInspection.csv
|   |   |   ├── Components.csv
|   ├── PICO_SMQ_QTM_Flexiway_SolarMuscleFlex_10112015
|   |   ├── BatteryExport
|   |   |   ├── BatteryExportData.csv
|   |   ├── VisualScreeningExport
|   |   |   ├── VisualScreeningExportData.csv
|   ├── PICO_LRC_QTM_Barefoot_FireflyMobile_15072012
|   |   ├── BatteryExport
|   |   |   ├── BatteryExportData.csv
|   |   ├── ExternalScreen1Export
|   |   |   ├── ExternalScreen1ExportData.csv
|   |   ├── ExternalScreen2Export
|   |   |   ├── ExternalScreen2Export1Data.csv
|   |   |   ├── ExternalScreen2Export2Data.csv
|   |   |   ├── ExternalScreen2Export3Data.csv
</pre>
As the test report template has changed over time, there have been minor changes in the file naming scheme. The software has been coded to account for those differences, so it is not necessary to change the names of specific test directories (e.g. "BatteryExport") or export files (e.g. "ExportData.csv").

## Outputs
### vbd.Rdata
The only output of this script is a Rdata file named "vdb.Rdata". This contains an r list object, "lighting.global.database", that will contain all product data in the data export after the script has been run.
#### Data Structure of lighting.global.database
lighting.global.database is an R list, with a list entry for each test Verasol performs on off-grid lighting products. Each list entry is an R data table object, containing all records for the given test, and can be accessed with the following R command:

lighting.global.database[['<test name<Sometimes Markdown is dumb>>']]

For example:
lighting.global.database[['Battery']]

The columns of each test-specific data table are directly taken from the test report spreadsheet, 

## Common Troubleshooting
Below are some troubleshooting techniques for common errors. Additional investigation may be required to find and fix certain issues.

### If the script crashes *before* the data export directory names are printed
This means that the error was not caused by a problematic data export directory, so the problem is somewhere in the script. Here are some common causes:

#### A file path is incorrect
If you get an error message reading "No such file or directory," the most likely culprit is a bad file path. Check the file name specified - you may also want to check any files paths stored in variables (i.e. "main.dir", "output.file.dir") to makesure there are no errors. If the issue persists, more detailed invrstigation will be needed.

#### If a function cannot be found (Again, make sound pretty)
If you get an error message reading "could not find function," this means that R does not recognize a called function. There are a few common causes:

##### 1. A module script didn't load properly
To keep the data consolidation script clean, many functions are contained in two separate module scripts: "consolidate_data_exports_functions.R" and "generic_functions.R". If either of these scripts did not load properly (this would be the first two lines of non-commented code, the "source" command), then thid error might happen. Check the file paths on the source commands.

##### 2. A library didn't load properly
If a library doesn't load properly, any functions within the library will be unavailable. Try running the appropriate load.libraries command again, otherwise more investigation might be needed.

##### 3. It wasn't meant to be a function
Functions in R are denoted by character strings followed by parentheses (for example, "list.files()"), whereas a specific index within a data structure (such as arrays, lists, and vectors) are denoted by character strings followed by brackets (for example, "test.results[1]"). So if parentheses are used instead of brackets on am R data structure, you will get a "could not find function" error.

### If the script crashes *after* data export directory names are printed
A data export might be faulty. Check for last directory printed for errors (the most common culprits are listed below), fix any identified issues, and re-run the script. NOTE: Sometimes there is no problem with the data export, the script just crashed (This would be the "machine just hates you" case referenced earlier). If you cannot find an error in the data export, re-run the script, and see if the issue persists.

#### Numbers as dates
Before data exports were data exports, they were Excel spreadsheets - and if the wrong column was formatted as a date, then you may find yourself with a value of "Jan. 1, 1900" where you expected to see a 1. Not surprisingly, this leads to issues when trying to perform any numerical analysis, and will likely crash the script. To fix this issue, you will either need to go back to the original spreadsheet, fix the formatting, and re-export, or if that is not possible, remove the offending data export and report to the broader team what happened.

#### Numbers as characters
Occasonally, numeric values are read as character strings instead of numbers - a leading space or a quotation mark are common culprits. This will also cause issues when performing numerical analysis. If you can remove any unwanted, non-numeric characters, the value should read as numeric on the next run.
