### Benson Challenge Report

#### Challenge 1 
For this first challenge, I downloaded several turnstile files from the MTA website.  I then created two scripts, the first to read the local files and the second to read off the MTA website.  In particular, I chose only data from 2015-2018, because from 2014-2015 the file format was changed pretty significantly.

#### Challenge 2 & 3
I saw these challenges as primarily a task of cleaning the data.  Here is a quick list of what I did:  

* I declared my own column names according to MTA help file (this allowed me not to waste time cleaning or changing names)  
* For time series, I turned `date` and `time` into `date_time`  
* Initially, I also dropped a lot of timestamps.  While, I later dropped this in order to finish deliverable, I thought this was an important step, thus code remains in Jupyter notebook file.  Since turnstile data is collected every 4 hours, a quick check revealed that the 4 6 hour-cycle times (12, 1, 2, 3am) contain most of the rider data.  Without filtering, there are thousands of unique timestamps.
* `lines` had a problem that was resolved by simply sorting each entry with a lambda function.
* Also found that `stations` only had ~360 values, while a quick Google search stated that MTA had 472 stations. To resolve this, I tried combining `station` and sorted `lines_sorted` to create new category `station_line`.  This gave me ~460 'stations', a drastic improvement.  
* Finally, I organized turnstile data by net entry/exit.  Each turnstile collects cumulative totals, but the real problem is that there are excessively large values AND negative values.  For the negative values, I assumed the turnstile reversed signs, and for the values exceeding 7000, I dropped those results.  A value of 7000 suggests that the single turnstile had roughly 1 person pass through every 2 seconds for a whole 4 hours, which seemed pretty unreasonable.


#### Challenge 4 
For this challenge, I took a single turnstile defined by `control`,`unit`, and `scp` from Grand Station.  In a previous iteration of this part of my code, I had narrowed down my results through time stamps, which was an inefficient method since I had to manually view the time stamps to know whether I had the right data or not.  For added understanding, I presented 3 graphs here, one for entries, one for exits, and one for total ridership (entries+exits).  

![Turnstile image](/station.png)


As can be seen, results are fairly predictable, with consistent dips in weekends.  Notably, there are two dips in weekdays on the 7 and 21, both of which were days where there was winter storms.  This will come back up again in a later graph.

#### Challenge 5 DONE

- So far we've been operating on a single turnstile level, let's
  combine turnstiles in the same ControlArea/Unit/Station combo. There
  are some ControlArea/Unit/Station groups that have a single
  turnstile, but most have multiple turnstilea-- same value for the
  C/A, UNIT and STATION columns, different values for the SCP column.

We want to combine the numbers together -- for each
ControlArea/UNIT/STATION combo, for each day, add the counts from each
turnstile belonging to that combo.


#### Challenge 6 DONE

Similarly, combine everything in each station, and come up with a time
series of `[(date1, count1),(date2,count2),...]` type of time series
for each STATION, by adding up all the turnstiles in a station.


#### Challenge 7 DONE

Plot the time series (either daily or your preferred level of granularity) for a station.


#### Challenge 8 DONE

Select a station and find the total daily counts for this station. Then plot those daily counts for each week separately.

To clarify: if I have 10 weeks of data on the 28th st 6 station, I will add 10 lines to the same figure (e.g. running `plt.plot(week_count_list)` once for each week). Each plot will have 7 points of data.


#### Challenge 9  DONE

- Over multiple weeks, sum total ridership for each station and sort
  them, so you can find out the stations with the highest traffic
  during the time you investigate


#### Challenge 10  DONE
I completed this task with a bar plot that displays the top 20 station lines ranked by traffic from March 18 through June 2018.  As an added bonus, I highlighted the top 8 by displaying them in coral, rather than default blue. 