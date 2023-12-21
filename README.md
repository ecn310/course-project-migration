## Migration Project Data
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

### Next Steps
- For further information about working with and displaying the data, refer to the "README expanded.md" file on this repository.
