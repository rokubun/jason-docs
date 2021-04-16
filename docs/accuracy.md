# Accuracy analysis

This section includes some accuracy analysis we have performed with Jason for
you to have an idea of which accuracy you can obtain with the service

## GNSS geodetic-grade receiver (static)

The purpose of this test was to assess the accuracy that can be achieved using
a geodetic grade GNSS receiver in static mode (non moving platform with 
static dynamics in the navigation filter).

|Test setup||
|:----|:------|
|GNSS receiver | Septentrio AsteRx|
|Antenna | Septentrio PolaNT |
|Environment | Rooftop, open sky, no multipath structures nearby |
|Data length |  2.34 hours |
|Sampling rate | 1 second |
|Local time | 2019 Nov 18  12:45:20.000 |

The test setup (performed at the rooftop of Rokubun's headquarter offices at the
MediaTIC building) is shown in the following picture:

![AsteRx test setup](images/septentrio_static_test_mediatic_updated.jpeg "AsteRx test setup")

The Septentrio AsteRx data has been processed with Jason with the following
main characteristics:

|Processing characteristics||
|:---|:---|
|Strategy| Post-Processing Kinematic (PPK)|
|Dynamics| static |
|Reference station | IGN BCLN (16km baseline) |

In order to assess the results, the same data file (converter to Rinex) has been
processed using [JPL APPS online Precise Post Processing](http://apps.gdgps.net/) (PPP) 
tool. The differences are shown in the table below:

|component| JPL APPS (ultra-rapid products) | Jason PPK | difference (vs JPL)|
|:---:|:---:|:----:|:----:|
| x       |    4787691.861     | 4787692.106 |     0.245 |
| y       |    183434.826      |  183434.274 |    -0.552 |
| z       |    4196130.151     | 4196129.589 |    -0.562 |

The **East/North/Up** difference between the two is -0.561 / -0.569 / -0.204 respectively.

**Note**: PPP results (JPL and NRCan) were performed with
ultra-rapid orbits (in the case of JPL) and also the data take was very short
(2h), which in the case of PPP can be a drawback in terms of convergence time.

## Smartphone (non-moving dynamic)

This test intends to provide an estimate accuracy of the best accuracy that can
be achieved with a smartphone in the most benign environment possible (non moving,
open sky, no multipath)

|Test setup||
|:----|:------|
|GNSS receiver | Xiaomi Mi 8 |
|Antenna | internal |
|Environment | Rooftop, open sky, no multipath structures nearby |
|Data length |  7 minutes |
|Sampling rate | 1 second |
|Local time | 2019 Nov 19  12:17 |

The smartphone was colocated on the same point at which the antenna of
[the static test](#gnss-geodetic-grade-receiver-static). The data was then
processed with Jason with the following processing strategy:

|Processing characteristics||
|:---|:---|
|Strategy| Post-Processing Kinematic (PPK)|
|Dynamics| Smartphone was not moving, but processed with kinematic stochastics |
|Reference station | IGN BCLN (16km baseline) |

![Easting/Northing error (smartphone dynamic)](images/mi8_ppk-kine_BCLN_enu.png "Easting/Northing error: Xiaomi Mi 8 (kinematic) - AsteRx(static)")
