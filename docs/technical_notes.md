---
title: Technical notes
author: Your name here
date: 2026-11-01
---


## Data

- Used MDPS Early Childhood Development dataset 
    - suppied by Emily DeMarinas (2026)
    - collection and updates were not documented 
- Removed rows without addresses.
    - This excluded the footnotes stored at the bottom of the CSV.
- Zipcodes
    - They are identifiers, not measurements, so keep them as text or factors.
    - No property or neighborhood data are included in the final charts.
- gen_program_setting_detail
    - Each program record has one setting.
    - Program types overlap, so grouping by type could count a record more times.
- Found 44 missing closing-time entries during exploration.
    - Excluded program-days without usable opening and closing times.
    - Other usable days from the same program could still be included.
    - Missing schedules do not mean the program is closed.
- Counts represnet program records. 
    - They do not measure capacity, vacancies, or enrollment. 

## Code

- libraries used:
    - ggplot2, for charts and styling.
    - dplyr, for filtering, calculations, and grouping data.
    - tidyr, used to structure the data and organize the scheudles. 
    - ggmosaic, used ofr mosaic chart
    - kitr::kable(), used to make markdown table.
- EDA = exploration 
- Sketchs = SKetching out improved charts 
- Final_draft = The final charts produced to be distributed. 
- Put the final preperations for all charts on the final notebook into a setup
  chunk. 
    - Runing that one setup before the charts prepares them all. 
    - each final chart has its own labeles 
- Created Setting_colors 
    - a color scheme assigned to the setting names so they would be the same for
      all charts. 
-Grouped records by zipcodes and settings. Each Program had such. 
    - use dplyr::n() to find counts.
    - print table with kitr::kable(format = "pipe")
    
# Mosaic
- Replaced the original stacked bar chart with a mosaic.
    - Segment heights show setting percentages within each ZIP.
   - Section widths generally show differences in record counts.
- Used pmax(total, 12) to enlarge small ZIP sections.
    - ZIPs with fewer than 12 records would otherwise be hard to see.
    - This changes the displayed widths, not the actual counts or setting 
      percentages.
    - Widths are therefore not exactly proportional to counts.
- Added actual counts before the ZIP labels.
- Sorted by ZIP before setting the label order.
    - Sorting the labels directly would sort by the count at the beginning.
  
# Heatmap
- Reshaped the opening and closing columns into one row per program-day.
- Converted times into numeric hours.
    - For example, 6:30 becomes 6.5.
- Created 24 hourly checks for each usable program-day.
    - Checks whether the program is open at the start of each hour.
    - Does not measure the share of the entire hour that it is open.
- Grouped by setting, day, and hour.
    - Averaged the open/closed checks and multiplied by 100.
- Added missing setting-day-hour combinations back for display.
    - Kept those percentages missing.
- Used the same grey for missing information and 0% open.
    - They look the same but remain different values in the data.

# Line chart
- Used the heatmap’s daily percentages.
- Grouped Monday–Friday as weekdays and Saturday–Sunday as weekends.
- Averaged daily percentages equally within each group.
    - Excluded missing values.
    - This is an average of daily percentages, not a combined count of all 
      programs.
- Used both color and line pattern to distinguish settings.
- Kept weekdays and weekends in separate panels with the same percentage scale.
  Saving and running
- Saved each chart with ggsave() as a PNG.
    - Filenames include green and a meaningful chart label.
- Used ../data and ../plots.
    - These paths assume execution from the code folder.
- Render the whole notebook after changes.
    - This checks that objects are created in the correct order.
    - Also check that captions and the one-row legends fit.

## Potential improvements / possible next steps

- Add setting totals to the mosaic legend.
    - Counts to the left of each color key.
    - Setting names to the right.
-Add light-grey backgrounds behind every other ZIP.
    - Would help connect labels to the mosaic sections.
- Give missing schedules a different color from 0% open.
    - Especially important for weekends.
    - Missing information should not look like confirmed closure.
        - this would change the weekends values. 
- show how many usable schedules contribute to each percentage.
    - Would make small groups easier to interpret.
- Improve overlapping lines.
- Could try separate panels for each setting or more distinct line patterns.
- The current calculation keeps both sides of midnight under the 
  listed program-day.
- A calendar-day comparison would need to move the after-midnight portion to 
  the following day.
- want to further examine affordability, vacancies, and family needs.
    - Would require additional data.


## Other notes

-A high percentage open does not mean many programs operating.
    The table and Mosaic are examples. 
-color names and arguments use diffrnet code a issue i had was that carto 
pallet uses "Bold"" and text styling "bold" that was confusing. 
- 
