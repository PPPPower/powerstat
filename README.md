# powerstat
Powerstat measures the power consumption of a machine using the battery stats or the Intel RAPL interface. The output is like vmstat but also shows power consumption statistics. At the end of a run, powerstat will calculate the average, standard deviation and min/max of the gathered data. 



http://manpages.ubuntu.com/manpages/artful/man8/powerstat.8.html


artful (8) powerstat.8.gz

Provided by: powerstat_0.02.12-1_amd64 bug

NAME

       powerstat - a tool to measure power consumption

SYNOPSIS

       powerstat [options] [delay [count]]

DESCRIPTION

       powerstat  measures  the  power  consumption  of  a computer that has a
       battery power source or supports the RAPL (Running Average Power Limit)
       interface.   The output is like vmstat but also shows power consumption
       statistics.  At the end of a run, powerstat will calculate the average,
       standard deviation and min/max of the gathered data.

       Note  that  running  powerstat  as  root will provide extra information
       about process fork(2), exec(2) and exit(2) activity.

OPTIONS
       powerstat options are as follow:

       -a     enable all statistics gathering options, equivalent to  -c,  -f,
              -t and -H.

       -b     redo  a  sample measurement if a system is busy, the default for
              busy is  considered  less  than  98%  CPU  idle.  The  CPU  idle
              threshold can be altered using the -i option.

       -c     gather  CPU  C-state  activity  and show the % time and count in
              each C-state at the end of the run.

       -d delay
              specify delay in seconds before starting, default is 180 seconds
              when running on battery or 0 seconds when using RAPL. This gives
              the machine time to settle down and for the battery readings  to
              stabilize.

       -D     enable  extra  power  stats  showing  all the power domain power
              readings. This currently only applies to the -R RAPL option.

       -f     compute  an  average  frequency  from  all  on-line  CPU  cores.
              Unfortunately  a CPU core is always active to gather any form of
              stats because powerstat has to be running to  do  so,  so  these
              statistics  are  skewed  by this.  It is best to use this option
              with a reasonably large delay  (more  than  5  seconds)  between
              samples to reduce the overhead of powerstat.

       -g     show  GPU power readings. Currently just Intel i915 is supported
              and one needs to run powerstat with root privilege to access the
              kernel i915 /sys debug interface.

       -h     show help.

       -H     show histogram of power measurements.

       -i threshold
              specify  the idle threshold (in % CPU idle) to force a re-sample
              measurement if the CPU is less idle than this level. This option
              implicitly enables the -b option.

       -n     no  headings.  Column  headings are printed when they scroll off
              the terminal; this  option  disables  this  and  allows  one  to
              capture the output and parse the data without the need to filter
              out the headings.

       -p     redo a sample measurement if any  processes  fork(),  exec()  or
              exit().

       -r     redo  if  system is not idle and any processes fork(), exec() or
              exit(), an alias for -p -b.

       -R     read power statistics  from  the  RAPL  (Running  Average  Power
              Limit)  domains.  This  is supported by recent Linux kernels and
              Sandybridge and later Intel processors.  This only  covers  some
              of  the  hardware in the machine, such as the processor package,
              DRAM controller, CPU  core  (power  plane  0),  graphics  uncore
              (power  plane  1) and so forth, so the readings do not cover the
              entire machine.
              Because  the   RAPL  readings   are   accurate   and   available
              immediately,  the  start  delay (-d option) is defaulted to zero
              seconds.

       -s     this dumps a log  of  the  process  fork(),  exec()  and  exit()
              activity on completion.

       -S     use standard averaging to calculate power consumption instead of
              using a 120 second rolling average of capacity samples. This  is
              only  useful  if the battery reports just capacity values and is
              an alternative method of calculating the power consumption based
              on the start and current battery capacity.

       -t     gather  temperatures from all the available thermal zones on the
              device. If there are no thermal  zones  available  then  nothing
              will be displayed.

       -z     forcibly  ignore  zero power rate readings from the battery. Use
              this to gather other statistics (for example when using -c,  -f,
              -t  options)  if powerstat cannot measure power (not discharging
              or no RAPL interface).

EXAMPLES
       Measure power with the default of 10 samples with  an  interval  of  10
       seconds
               powerstat

       Measure power with 60 samples with an interval of 1 second
               powerstat 1 60

       Measure  power  and  redo  sampling  if  we  are not idle and we detect
       fork()/exec()/exit() activity
               sudo powerstat -r

       Measure power using the Intel RAPL interface:
               powerstat -R

       Measure power using the Intel RAPL interface and show extra RAPL domain
       power readings and power measurement histogram at end of the run
               powerstat -RDH

       Measure power and redo sampling if less that 95% idle
               powerstat -i 95

       Wait  to  settle  for  1 minute then measure power every 20 seconds and
       show any fork()/exec()/exit() activity at end of the measuring
               powerstat -d 60 -s 20

       Measure temperature, CPU frequencies, C-states, power via RAPL domains,
       produce histograms, don't print repeated headings and measure every 0.5
       seconds
               powerstat -tfcRHn 0.5

SEE ALSO
       vmstat(8), powertop(8), power-calibrate(8)

AUTHOR
       powerstat was written by Colin King <colin.king@canonical.com>

       This manual page was written by Colin King  <colin.king@canonical.com>,
       for the Ubuntu project (but may be used by others).

COPYRIGHT
       Copyright © 2011-2016 Canonical Ltd.
       This is free software; see the source for copying conditions.  There is
       NO warranty; not even for MERCHANTABILITY or FITNESS FOR  A  PARTICULAR
       PURPOSE.

                                16 August, 2015                   POWERSTAT(8)
