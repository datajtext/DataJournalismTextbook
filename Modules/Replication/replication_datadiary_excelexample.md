# A simple data diary

A simple data diary for the [beginning of the Excel math review module](../MathReview/mathreview_with_excel.md) might look something like this:

### Data source

Original file downloaded as a xx-page PDF from the Phoenix city budget site at https://www.phoenix.gov/budgetsite . The link was https://www.phoenix.gov/budgetsite/Budget%20Books/SummaryBudget2017-18.pdf. It's undated as far as I can tell.

The key tables were on pages 182-183 -- that is listed as the "Expenditures" by program.

Using Acrobat, extracted out those pages into a new file, ~/Documents/examples/ phx_budget_2017_table.pdf

I tried to extract the tables using different programs: Able2Extract, Adobe Acrobat, Tabula. Then I realized that it is an image, not a text, pdf. Went back and OCR'd it using Adobe Acrobat, but when I sent it to a csv, it was a mess.

I decided to type in the numbers myself rather than try to clean it up.

### The original spreadsheet
Created a blank spreadsheet called ~/Documents/examples/phx_budget_summary.xlsx .
Added a notes page to document where I got it from.

categories sheet: Typed in the numbers from the 2016 actual, 2017 estimated and 2018 budget category totals.

Selected them and checked against the totals shown at the bottom of the page. They were right, except for 2018. Then I realized I hadn't typed in the "contingency" line. I decided not to type it in at all.

Did the same thing for the individual programs on another sheet, but entered the categories into their own column, in a tidy fashion.

Checked against the originals. They matched. Made sure to un-format any numbers so that if I want to export to another program, they'll come in correctly.

This spreadsheet won't be changed unless the data is updated.

### Cleanup

Formatted the numbers as dollars.

Widened the columns

Added a unique identifier to the detail rows in categories in case I need to sort.

Created a row that checks the sums of the detail against the sum provided by the city.

Saved the spreadsheet as phx_budget_summary_sc01.xlsx

### Questions

* What is the money for contingency? How has it been used in the past?
* What does "estimated" mean for 2017 -- don't they know how much was actually spent? When was this created?
* Is there any reason that comparing the estimated 2017 to budgeted 2018 would be misleading?

### Keep going

You can finish the rest yourself, but the key is that everything you've done is logged, and anyone reading this can follow what you did. Including yourself.
