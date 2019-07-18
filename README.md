# Wage Gap PUMS
R code to generate confidence measures for wage gap analysis
This tutorial explains how to download ACS microdata from IPUMS, generate confidence measures in R, and visualize the data with Tableau for a wage gap analysis.

Download and extract the data from IPUMS

Select which sample year you want to use and whether it’s 1 year or 5 year data (5 year data recommended)

•	Select the following variables for your extract:

o	Household>Geographic: MET2013 (or other geography variable)

o	Person>Technical: REPWTP (replicate weights)

o	Person>Demographic: SEX, AGE

o	Person>Race, Ethnicity & Nativity: RACE, HISPAN

o	Person>Work: OCC2010, WKSWORK2 (weeks worked last year), UHRSWORK (usual hours worked per week)

o	Person>Income: INCWAGE (wage and salary income)


•	On the create extract page:
o	Change data format from .dat to .csv
o	Select cases to limit age to 16+ and geography to Portland MSA (this reduces the size of your extract)
•	Once you can download your extract from IPUMS – it will be in .gz format
•	Convert the .gz file online using https://extract.me/ - will extract to .zip format
•	Extract downloaded .zip file and open folder
•	Change the file’s extension to .csv and open it to confirm it’s working and contains all your variables
Calculate Standard Errors and Coefficient of Variation with R
•	Run R code to produce a .csv with the standard errors (SE) for your desired variables
•	Calculate coefficient of variation (CV) = SE/Total Employment
•	Copy CV sheet into full PUMS file and save in Excel format to import into Tableau
•	You can delete replicate weight columns from the Excel file you’re importing to Tableau to save on file size 
Visualize the Data with Tableau
•	Connect CV sheet to PUMS file on Occ2010 and Sex (inner joins)
•	Go to Sheet 1. Convert Occ2010 and Sex to Dimension (from PUMS file). Double click Occ2010, Sex, Perwt, and Incwage to populate the crosstab. Right click SUM(Incwage) > Measure(Sum) > Median.
•	Add filter where CV is less than or equal to 0.4 by dragging the CV to the Filters pane. Select All Values > up to 0.4 > Apply > OK.
•	Right click on MEDIAN(Incwage) > Quick Table Calculation > Difference. The pill will change to include a triangle to indicate a table calculation. Drag the pill back to the measures sidebar. It will appear as “Calculation1”. Change the name to Wage Gap. Drag the original Incwage pill back to the Measure Values pane and change from Sum to Median. This will then show the median wage and the wage gap by occupation.
•	To view the total difference in wage, click Analysis > Totals > Show Column Grand Totals. The totals will appear at the bottom of the crosstab. You can change this to the top of the crosstab by clicking Analysis > Totals > Column Totals to Top.
•	For full-time, year-round: drag UHRSWORK to filters (All Values > greater than 35) and drag WKSWORK2 to filters (All Values > equals 6)
•	To convert to a chart, duplicate the sheet. Remove Sex and Measure Names from the columns and rows. Drag Incwage to Columns twice and change both from SUM to MEDIAN as above. Right click the second MEDIAN(Incwage) > Dual Axis. On the Marks card, select the first MEDIAN(Incwage). Drag Sex from the sidebar onto Color. Select the second MEDIAN(Incwage) and change the drop down from Automatic to Line. Drag Sex from the sidebar onto Path. Select All on the Marks card and remove Measure Values. Your dots and lines may be misaligned. Right click the horizontal axis > Synchronize Axis.
For Race/Ethnicity
•	Run R code to generate CVs for white and people of color workers
•	In your PUMS file, add a column to label each worker as white or poc (IF statements work well for this).
•	Save in Excel format to import into Tableau
•	Connect Race CV sheet to PUMS file on Occ2010, Sex, and Race/Ethnicity (inner joins)
•	Continue steps to analyze the data as above, adding Race/Ethnicity as a variable to analyze.
