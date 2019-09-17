# Welcome to Jason PaaS docs

Jason is Rokubun's Positioning-as-a-Service (PaaS), a cloud service to compute
the position of a rover using the raw GNSS raw measurements.

GNSS raw measurements are fundamentally pseudoranges and carrier-phases, which
are the observations used to obtain the position of a GNSS receiver.

Jason works on a best-effort basis: it will attempt to compute the best possible
solution using a differential technique known as Post-processing Kinematic (PPK), 
which is the post-processing version of the Real Time Kinematics (RTK). These
techniques combine GNSS measurements from nearby  **reference stations** with
those of the rover being positioned to cancel out most of the. By nearby it
is usually considered less than 30km apart.

## Coverage

The data from the reference stations come from a set of world-wide public providers such
as [International GNSS Service](https://www.igs.org) or [EUREF](http://www.epncb.oma.be/) as
well as smaller national and regional networks such as the [Institut Cartogràfic i Geològic de Catalunya](https://www.icgc.cat) and the like.

In total, we continously monitor the availability of more than 10000 stations
distributed worldwide. Some areas are better covered than others but unfortunately
we cannot provide global coverage.
