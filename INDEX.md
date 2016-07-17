# This index goes over the purpose of each file in the project

## Management

- bin/loop - runs bin/run every 3500 seconds (for running under tmux or supervise - use runX/run-cron for a crontab)

- run\*/run-cron - use this script to generate your graphs from cron

- bin/run - pulls logfiles, filters and converts them, splits them apart, and then calls bin/plot

- bin/copy-logfiles - script to copy the ntp logfiles from a remote system (optional, see example)

- bin/copy-to-website - copies the html and png files to your website (see example)

## Graphing

- bin/plot - generates graphs. Calls: local-clock-graph, offset-graph, skew-graph, custom-plot, copy-to-website, and data transformation programs
 - generates: percentiles.png
 - generates: percentiles-offset.png
 - generates: offset-histogram.png
 - generates: gps-lock.png (optional)
 - generates: gps-snr-hourly.png (optional)
 - generates: gps-snr-cdf.png (optional)

- bin/local-clock-graph - generates graphs for the local clock stats
 - generates: local-clock.png
 - generates: local-clock-stddev.png
 - generates: local-clock-skew.png

- bin/offset-graph - generates graphs for remote and refclocks
 - generates: all-offset.png
 - generates: remote-\*.png

- bin/skew-graph - generates a clock skew (clock changes in rate) graph for remote clocks and refclocks
 - generates: all-skew.png

- bin/foreach-stat - generates gnuplot commands for each remote clock and refclock

- bin/graph-header - generates gnuplot header commands

- run\*/custom-plot - optional script, create it with your custom plot commands

## Data Transformation

- bin/cumulative - generates a cumulative count, takes a column # and step. used to generate the CDF

- bin/histogram - generates a histogram count, takes a column # and multiplication factor. rounds to the integer nearest 0

- bin/histogram-snr - generates a histogram count from GPS SNR data

- bin/index - used to replace tokens in index.html.tmpl to produce index.html

- bin/minmax - takes a column # and either "min" or "max" - prints the min or max for that column

- bin/mul - takes a number as an argument, multiplies stdin by it, and prints it out

- bin/percentile - takes a column # and a percentile, prints out that percentile of the data

- bin/snr-hourly - takes GPS SNR data and prints out the count of messages SNR=0 and SNR!=0 were seen

- bin/split - splits logfiles into one logfile for each source clock

- bin/timestamps - convert NTP logfile timestamps into unix integer timestamps (%s strftime format)

- bin/timestamps-chrony - converts Y-M-D H:M:S timestamps to unix integer timestamps (%s strftime format)

## Running files

- run\*/index.html.tmpl - this file is used to generate index.html, change this file instead of index.html

- run\*/notes - this file gets added near the end of index.html, use this to track changes to your setup
  - example: "Jun 18 01:21 - rebooted, new kernel module"

- run\*/startime - optional script to tell bin/run what times to filter out (see example)

- titles - gives a name to each refclock/remote clock

- aliases - use this to combine source names if your remote clock has multiple addresses (ex: v6+v4 or DNS based load balancing)
