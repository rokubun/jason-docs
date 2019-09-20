# GNSS data processing strategies

There are multiple strategies to process GNSS raw measurements in order to 
obtain the position. The most common ones are:

- Single Point Positioning (SPP)
- Precise Point Positioning (PPP)
- Real Time Kinematics (RTK)
- Post-processing Kinematics (PPK)

With the advent of new constellations and the inflationary number of additional
signals and frequencies (between the original L1 and L2 from GPS) as well as
the requirements of convergence time in dynamic scenarios, new techniques based
on innovative data models (such as undifferenced and uncombined processing) or
a combination of classic techniques (PPP-RTK) are gaining relevance in front
of these.

| strategy | needs base? | uses carrier-phase? | orbits & clocks | accuracy |
|:--------:|:-----------:|:---------------:|:---------------:|:--------:|
| SPP      | no          |    no           | broadcast       |    < 5 m |
| PPP      | no          |    yes          | precise         | cm (multi-freq), dm (single-freq)|
| RTK      | yes         |    yes          | broadcast       | cm (multi-freq), dm (single-freq)|
| PPK      | yes         |    yes          | broadcast       | cm (multi-freq), dm (single-freq)|

- _needs base?_ implies if the technique is a differential technique
