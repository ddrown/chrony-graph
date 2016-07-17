# Definitions

- clock offset = the difference between the actual time and the local clock's time. (Also can be called phase offset)
- frequency offset = the difference between the local clock's actual frequency and its expected frequency (usually in parts per million, ppm)
- jitter = the short term change in a value
- ms, millisecond = one thousandth of a second
- ppm, parts per million = Ratio between two values. These following are all the same: 1 ppm, one in one million, 1/1000000, 0.000001, and 0.0001%
- refclock = reference clock, from a GPS module or other source of time
- remote clock = clock reached over the network, LAN or WAN
- upstream clock = any remote clock or reference clock used as a source of time
- us, µs, microsecond = one millionth of a second, and one thousandth of a millisecond
- wander = the long term change in a value
- SNR = signal to noise ratio.  Higher values indicate a strong signal. values over 20dB are good
- CDF = cumulative distribution function.  Another way of looking at a histogram, it shows how likely a given value is

# NTP Graphs generated and what they mean

- Graph Title: "Local Clock Offsets"
 - filename: local-clock.png
 - This graph can be used to see the relationship between the frequency offset of the local clock (red, in parts per million, right) against the local clock offset.  Quick changes in frequency will lead to larger clock offsets.

- Graph Title: "Local Clock Frequency Offset"
 - filename: percentiles.png
 - This shows the frequency offset of the local clock.  It includes percentile data to show how much the frequency changes over a longer period of time.  The majority of this change should come from temperature changes (ex: HVAC, the weather, CPU usage causing local heating).
 - Smaller changes are better.  An ideal clock would be a flat line at 0ppm.
 - Expected values: +/- 500ppm
 - Expected values of 99%-1% percentiles: within 10ppm

- Graph Title: "Local Clock Time Offset"
 - filename: percentiles-offset.png
 - This shows the clock offset of the local clock.  It includes percentile data to show how close the local clock is to its upstream clocks.  This can be affected by: precision of the upstream clock, accuracy of the upstream clock, changes in the local clock frequency offset.
 - Values closer to 0 are better.  An ideal system would be a flat line at 0us.
 - Expected values for GPS refclock systems: 99% and 1% percentiles within +/- 10us
 - Expected values for internet upstream clocks: within +/- 10ms (this depends on your internet connection quality)

- Graph Title: "Local Clock Time Offset - Histogram"
 - filename: offset-histogram.png
 - This shows the clock offsets of the local clock as a histogram.  It includes 1%, 25%, 75%, and 99% percentiles to show the performance of the system.  

- Graph Title: "RMS Frequency Jitter - ADEV aka wander"
 - filename: local-clock-skew.png
 - This shows the jitter of the local clock's frequency.  In other words, how fast it the local clock changes freqency.
 - Lower is better.  An ideal clock would be a straight line at 0ppm.

- Graph Title: "RMS Time Jitter"
 - filename: local-clock-stddev.png
 - This shows the jitter of the local clock offset.  In other words, how fast the local clock offset is changing.
 - Lower is better.  An ideal system would be a straight line at 0us.

- Graph Title: "all clocks (offset)"
 - filename: all-offset.png
 - This shows the offset of all remote clocks and refclocks.  This can be useful to see if offset changes are happening in a single clock or all clocks together.
 - Closer to 0us is better.  An ideal system would be a straight line at 0us.

- Graph Title: "all clocks (skew)"
 - filename: all-skew.png
 - This shows the jitter of the remote clock offset.  In other words, how quickly the remote clock offset is changing.
 - Closer to 0us/s is better.  An ideal system would be a straight line at 0us/s.

- Graph Title: "offset of X"
 - filename: remote-\*.png
 - This shows the clock offset between the local clock and a remote clock or refclock.
 - For remote clocks, the purple line is the offset while the green and blue lines are the request and response.  The request and response lines can show if the change in offset was due to an asymmetric network effect (either request or response latency went up/down, but not both), a symmetric network effect (request and response latency went in opposite directions), or the clocks changed in offset (request and response and offset all went in the same direction).
 - The orange 50th percentile line shows the median offset value.  You can use this to align offsets between LAN stratum 1 servers.

# GPS Graphs generated and what they mean

- Graph Title: "% of time spent in GPS lock"
 - filename: gps-lock.png
 - optional, depends on the ntp-www logfiles
 - Shows the % of time the GPS module was in 2D or 3D lock.  Useful to see if your GPS has a good signal

- Graph Title: "Percent of time satellites spent at 0 snr"
 - filename: gps-snr-hourly.png (optional)
 - optional, depends on the ntp-www logfiles
 - shows the % of time the GPS satellites were at 0 SNR (no signal received).  Useful to see if your GPS has a good signal

- Graph Title: "GPS SNR cdf"
 - filename: gps-snr-cdf.png (optional)
 - optional, depends on the ntp-www logfiles
 - shows a distribution of SNR values.  Useful to compare GPS antennas.  The line shows how often the satellites were at a given SNR or lower.
