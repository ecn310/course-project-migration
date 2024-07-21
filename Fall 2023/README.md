# Migration Project Data
- ***A description of these data downloading, viewing, and coding steps may be found in our [report](https://github.com/ecn310/course-project-migration/blob/main/Migration%20Report%20Final.pdf).***
## Downloading and viewing the data
- ***Our downloaded data extracts are located in this [OneDrive folder](https://sumailsyr-my.sharepoint.com/:f:/g/personal/qwu102_syr_edu/EkqFuAJIbdFPkJEZ4kzdPa0B8dHyLAJbPNibAs3KxNpevg).***
### Generating data extracts on IPUMS
- Sign in (create an account if you don't have one) to the [IPUMS USA](https://usa.ipums.org/usa/) website.
- Click on "Select Data," then select the desired samples and variables.
- There are 8 samples that we worked with in our project, one for each year from 1950 to 2020:
>- 1950 1% sample
>- 1960 5% sample
>- 1970 1% metro fm1 sample
>- 1980 1% metro sample
>- 1990 1% metro sample
>- 2000 ACS sample
>- 2010 ACS sample
>- 2020 ACS sample
- We chose the following variables in our project:
>- race (RACE)
>- total personal income (INCTOT)
>- CPI deflator (CPI99)
>- birthplace (BPL)
>- place of residence 1 year ago (MIGPLAC1) or place of residence 5 years ago (MIGPLAC5)--this variable depends on availability
- Once the data extracts are created, download (1) the data file and (2) the Stata command file.

### Accessing the data
#### the data (.dat) file
- The data file will be compressed when first downloaded from IPUMS.
- Extract the data file, using an external application to do so if necessary. (We used 7-Zip to help us extract the data files.)

#### the command (.do.txt) file
- The command files can be opened directly in Stata once downloaded.
- Open Stata, then open a new do-file editor.
- Click "Open" and select the command file that you just downloaded from IPUMS.
- Add the "cd" command to the top of the command file to set the file to your own working directory.
- If you changed the name of the data file, make sure to also change the line of code that uses that data file name to open the data.

#### Putting it all together (Viewing the data)
- After extracting the data file and making the necessary adjustments to the command file, run the entire command file. The data should now be viewable in Stata.

## Working with the data
- ***Our modified do-files are located in this [OneDrive folder](https://sumailsyr-my.sharepoint.com/:f:/g/personal/qwu102_syr_edu/EkqFuAJIbdFPkJEZ4kzdPa0B8dHyLAJbPNibAs3KxNpevg). There is one do-file for each sample year (decades from 1950-2020), each of which has a version of the following codes added to the end.***
### Finding the median income
- gen realinc=inctot*cpi99
  >- This makes sure that all dollar values are converted to the same base year (1999), which allows for comparisons between different years.
- keep if realinc <9999999
  >- This eliminates all the numbers that are too large to be displayed by Stata.
- sort race
  >- This allows for the data to be later sorted by race.
- sum realinc, detail
  >- This provides a detailed summary of the real income of the total population, including the median (50th percentile) income, which is what we are looking for.
- by race: sum realinc, detail
  >- This provides a detailed summary of the real income of each racial group (e.g., Black people, White people, etc.), including the median income.

### Finding the migration rate
- gen north=0
  >- This generates a dummy variable that will later help to identify those individuals who were born in the North.
- replace north=1 if bpl==09
  >- This will help to identify individuals who were born in the North by specifically identifying each Northern state.
  >- 09 is the FIPS code for Connecticut. Repeat this line of code, replacing the 09 with the FIPS code for each of the remaining states identified as being part of the North: Delaware (10), Maine (23), Maryland (24), Massachusetts (25), New Hampshire (33), New Jersey (34), New York (36), Pennsylvania (42), Rhode Island (44), and Vermont (50).
- gen south=0
  >- This generates a dummy variable that will later help to identify those individuals who lived in the South one or five years prior to the sample year.
- replace south=1 if migpac1==01
  >- This will help to identify individuals who were born in the North by specifically identifying each Northern state.
  >- 01 is the FIPS code for Alabama. Repeat this line of code, replacing the 01 with the FIPS code for each of the remaining states identified as being part of the South: Arkansas (05), Florida (12), Georgia (13), Louisiana (22), Mississippi (28), North Carolina (37), Oklahoma (40), Tennessee (47), Texas (48), and Virginia (51).
  >- If the MIGPLAC1 variable is not available in a specific sample, use the MIGPLAC5 variable instead, repeating the same steps: replace south=1 if migplac5==01
- gen migsouth=0
  >- This generates a dummy variable that will combine the previous two.
- replace migsouth=1 if north==1 & south==1
  >- This combines the previous two dummy variables to help identify people who both were born in the North and lived in the South one or five years prior to a sample year. Finding the frequency of these individuals will help us to get the migration rate.
- tab migsouth
  >- This code displays the frequency and percentage of the total population who have a value of migsouth=0 or migsouth=1 assigned to them. The migration rate we want to collect is the percentage of migsouth=1. 
- by race: tab migsouth
  >- This does the same thing as the previous line of code, but for each racial group instead of for the total population.

## Displaying the data (using Excel)
- ***The Excel workbook we used to generate our graphs, as well as saved PNG files of the graphs themselves, are also located in our [shared OneDrive folder](https://sumailsyr-my.sharepoint.com/:f:/g/personal/qwu102_syr_edu/EkqFuAJIbdFPkJEZ4kzdPa0B8dHyLAJbPNibAs3KxNpevg).***
- In an Excel file, create two tables. Each table should have columns for each sample year (decades from 1950-2020, inclusive) and rows for each racial group (Black, White, and total). One table should be for median income, and the other table should be for migration rate.
- As each piece of data is collected (from Stata), record it in the appropriate
- Rearrange the two tables by racial group (instead of by what data they display, like they are currently). There should now be three tables.
- Select each table individually, and for each one, generate a graph (any type).
- Then, select the generated graph and click on the button that says "Change Chart Type." Choose the "Combo" option, then "Custom Combo." Make each series a line graph with markers.
- Add chart and axis titles for each graph as appropriate.
