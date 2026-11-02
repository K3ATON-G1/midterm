---
title: Technical notes
author: Your name here
date: 2026-11-01
---


## Data

- Used MDPS Early Childhood Development dataset 
  - suppied by Emily DeMarinas (2026)
  - collection and updates were not documented 
- Zipcodes
  - For geographic comparisn and agrication into groups 
  - used as idenifers.
- gen_program_setting_detail
  - Each program had a single setting, 1 of 5. Program types overlap witch 
  could count the same reocurs twice.
- Exluded the program days that had unfilled opening and closing days (44)

## Code

- librarys
  - ggplot2
  - dplyr
  - tidyr
  - ggmosaic
-Setting_colors 
  - a color scheme assigned to the setting names so they would be the same for
  all charts. 
-Grouped records by zipcodes and settings. Each Program had such. 
  - use dplyr::n() to find counts.
  - print table with kitr::kable(format = "pipe")
-replaced EDA and Sketch stacked bar chart with mosaic .
-gave missing inofration and 0% the same colors and counted all the data as 
missing not null. 

## Potential improvements / possible next steps

-add setting totals to the legend of the mosaic put on the left of the color
key and the setting type of the right of the legend color key. 
-clear up the data and show that the missing data and 0% are different on the 
map. For the weekends there was tons off missing and that was assigned to be 
the same as the days times with 0%. This may not be the best way to interpret 
the data. 
-the linechrat overlaps a lot and isn't very clear, ajusting the lines would be 
good. 

## Other notes

-A high percentage open does not mean many programs operating. Mosaic. 
-color names and arguments use diffrnet code a issue i had was that carto 
pallet uses "Bold"" and text styling "bold" that was confusing. 
