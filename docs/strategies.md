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

- _needs base?_ implies if the technique is a differential technique (requires
  the provision of GNSS data from a base station with known coordinates)
- _uses carrier-phase?_ the carrier-phase is required to achieve decimeter or
  centimeter accuracy.
- _orbits & clocks_ which type of orbit and clock products does the technique
  require.
- _accuracy_ is a ballpark indicator of the accuracy that can be achieved for
  the strategy.

Besides the technique to process data itself, one can inform the filter wether
the rover moves (**dynamic**) or stays still (**static**). This can be
configured in Jason: select only static if you are sure the receiver was not
moving during the data campaign, otherwise leave the default, which assumes
a moving (dynamic) rover.

Finally, please consider that the **number of frequencies** tracked by the receiver
might be crucial in terms of performance. For standalone techniques (SPP, PPP), which 
do not require base station, tracking 2 or more frequencies will allow to remove
the ionosphere error, leading to greater accuracies. In general however, and
this is valid for all strategies, tracking multiple frequencies will provide not
only better accuracies but also increased level of robustness and faster convergence
times.
