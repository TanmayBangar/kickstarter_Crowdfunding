# Crowdfunding (Kickstarter) Analysis

I analysed 365,892 Kickstarter projects to answer a simple question: what
makes a crowdfunding campaign succeed? I built the analysis in Excel,
rebuilt it in Tableau,and wrote the same queries in SQL.

What I did

1.Cleaned and prepared the data
- The date columns were stored as Unix timestamps,so I converted them to
  real dates and times
- Loaded the four tables (Projects,Category,Location,Creators) through
  Power Query
- Removed blank trailing rows and handled empty successful_at values so
  they didn't turn into fake 1970 dates

2.Built a calendar table
- Generated a continuous date list from the earliest to the latest project
  date
- Added Year,Month number,Month name,Quarter,Year-Month,Weekday
  number and name,Financial Month(April = FM1) and Financial Quarter
- Related it to the project data in Power Pivot through a date-only column

3. Added calculated columns
- Goal in USD (goal × static USD rate)
- Goal range buckets: 0-1K,1K-5K,5K-10K,10K-25K,25K-50K,50K-100K,
  100K-1M and 1M+
- Days taken to reach the goal for successful projects

4.Built the KPIs and dashboards
- Projects Overview:projects by outcome, location, category, and
  year / quarter / month
- Successful Projects:amount raised,backers,average days to
  succeed, and top 5 projects by backers and by amount raised
- Success rate:overall,by category,by year,and by goal range
- KPI cards,charts and slicers (year and country) across both pages

5.Rebuilt it in Tableau
- Related the tables, converted the timestamps with calculated fields,
  and rebuilt the charts
- Added dashboard filters and click-to-filter actions

6.Wrote it all in SQL
- Every question above as a query, including the calendar table, goal
  brackets and success percentages

What I found
- Only 38.35% of projects reached their goal (140,313 successful
  vs. 188,239 failed)
- Smaller goals win.Success rate drops from 52%  for goals under
  $1K to 1.2% for goals over $1M
- Tabletop Games succeed most often (62%);Appsleast (6%)
- The USaccounts for about 73% of all projects
- Successful projects raised $3.48B and took about 32 days on
  average to hit their goal
- The most funded project was Pebble Time ($20.3M); the most backed
  was Exploding Kittens (219,382 backers)

Problems I ran into and fixed
- My "Top 5 by amount raised"chart was sorted by backer count,so it
  showed the wrong projects,I fixed the Top-N filter
- The "Successful Backers" card was linked to the same value as "Total
  Backers",so I gave it its own measure
- My calendar ended one day before the data did, which left 2 projects
  without a date. I rebuilt it from the true maximum date
- The `static_usd_rate` column is 1 or 0 for many rows, so the goal in
  USD is only approximate
- Project country and location country disagree for about 5% of rows,so
  I used one field consistently

Tools
Power Bi Power Query, Power Pivot, DAX,SQL
