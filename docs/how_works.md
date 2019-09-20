# How does Jason works?

## Processing engine

Currently, Jason is a series of wrappers around the open-source package 
[rtklib](http://wwww.rtklib.com) that offers the possibility, among other tools,
to process the data using the 4 techniques mentioned above.

As mentioned, Jason works on a best-effort basis, and attemps to run these
[processing strategies](strategies) in the following prioritized order:

- _PPK_, Jason computes a coarse estimate of the rover position using _SPP_ in
  order to select the closest base station from the set of stations that we
  continuously track. If a nearby station is found (less than a certain baseline),
  then the corresponding RINEX data is downloaded in order to perform differential
  positioning.
- _PPP_, if no reference data is found, Jason will attempt PPP if the precise
  orbits and clocks for the day to be processed are found.
- _SPP_, if _PPP_ could not be performed, the data will be processed using
  the broadcast orbits and clocks.

## Supported formats

Jason supports the following input formats for to input GNSS observables
(pseudorange, carrier-phases, ...):

- Rinex 2/3
- U-blox formats (both single and multiple frequency formats)
- Data from Rokubun's receivers (Argonaut and Medea, which are Ublox-based, but
  also adding IMU and Event data)
- [Google's Android GNSS logger](https://github.com/google/gps-measurement-tools/tree/master/GNSSLogger) (smartphone data)
- RTCM 3 data
- Septentrio binary files
