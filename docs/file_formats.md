# File formats

This section include the information of the various file formats delivered by
the service.

## GNSS processor files

When a process has been successful, a compressed (ZIP) file is generated with all the
results of the process. The format of the different files included in the bundle
by the GNSS processor are described in the following sub-sections.

### Position files (csv)

Positions will be delivered as a comma separated file where the first line is
a comment (starts with `#`) with a description of the fields, which are:

- columns 1-2: **Epoch** of the solution, expressed as GPS week and seconds within the GPS week.
- columns 3-5: **Position** in WGS84 reference frame (latitude, longitude and height). 
                longitude and latitude expressed in decimal degrees and height in
                meters above the WGS84 ellipsoid.
- columns 6-8: Standard deviation in meters of the North, East and Up components.
                Note that these values are the formal **errors** delivered by the
                position filter (i.e. square root of the postfit variances) and
                they do not necessarily reflect the actual error in the
                navigation solution. The surveyor will need an external reference
                to compute the actual error. However, these values can be
                treated as a preliminary quality metrics of the solution.

Jason will always delivered the position file corresponding to the SPP
strategy (files ending with `_spp.csv`). If a more accurate sterategy
(PPP or PPK) could be performed, additional CSV will be also delivered,
ending with either `_ppp.csv` or `_ppk.csv`, to indicate the strategy
of the solution.

Example:

```csv
# GPSW,GPSSoW,latitude(deg),longitude(deg),height(m),sdn(m),sde(m),sdu(m)
2069,124585.300000,41.3495230130,1.6680445200,246.06570,2.3403,1.5631,4.6059
2069,124585.400000,41.3495233800,1.6680436110,246.40920,2.3403,1.5631,4.6059
2069,124585.500000,41.3495239180,1.6680507170,246.51000,2.3403,1.5631,4.6058
2069,124585.600000,41.3495241180,1.6680519850,246.22500,2.3403,1.5631,4.6058
2069,124585.700000,41.3495263560,1.6680520780,246.36660,2.3403,1.5631,4.6058
2069,124585.800000,41.3495281560,1.6680502930,245.82960,2.3404,1.5631,4.6058
2069,124585.900000,41.3495297610,1.6680474000,245.42580,2.3404,1.5631,4.6058
```

### Position files (kml)

For convenience, the positions are conveted to [KML format](google kml format) and included in the
ZIP package as well. These files can be easily opened using tools such as
[Google Earth](http://www.google.com/earth), just double-click on the files
and the application will open the file.

Similarly to the case of the CSV files, the KML corresponding to the SPP
strategy will be always delivered. If PPP or PPK has been successful, the
KML files for this strategy will be also delivered. The strategy will be part
of the file name.

In addition, for quick visualization, a **decimated version of the KML** file is
also provided. This is useful for a quick preview of files that have been 
taken in long data campaigns.

In case of **static** receivers, only the last point of the processing will be
included in the KML file.

### Plots (png)

As a visual summary of the processing task, a series of plots (in PNG format)
are also included in the bundle. These files are:

- `height.png`: Time series of the height above the WGS84 ellipsoid (in meters).
- `skyplot.png`: Skyplot showing the distribution of the satellites that have
                 been used for the processing. The points in the plot have
                 different color coding, depending on the constellation. Also,
                 the satellite ID is also shown at the last point, which is a
                 helper to know the direction to which the satellite moved.
- `num_satellites.png`: The time series of the number of satellte during the
                processing. The same color coding used in the skyplot has been
                used here. The chart is a stack plot and shows the number of
                satellites, at each epoch, of each constellation.

### Time/Camera events (csv)

In the event that the input contained time events (usually generated from
camera trigger), the output package will also contain a camera event file
`camera_events.csv`. The file contains as many rows as time triggers (camera
events) detected in the input file. Each row of the file contains the time tag,
position and formal error of the camera event, with the same format as 
described above for the CSV files.

## GNSS converter files

### Argonaut IMU file

Rokubun's Argonaut/Medea receivers store GNSS data as well as IMU data from its
inertial sensor. This **data is syncrhonized** with the GPS time scale and stored
in the SD card along with the GNSS raw measurements. When using the conversion
tool from Jason, a CSV file with the IMU data will be generated. The file starts
with a comment line (starting with `#`) that describes each column as well as
the appropriate units:

- `GPSWEEK` The GPS week of the time stamp
- `GPSTOW` The seconds of the GPS week
- `MAGX`, `MAGY`, `MAGZ`, 3 components (XYZ) of the magnetometer, expressed in nano-Teslas
- `GYRX`, `GYRY`, `GYRZ`, 3 components (XYZ) of the gyroscope, expressed in degrees per second
- `ACCX`, `ACCY`, `ACCZ`, 3 components (XYZ) of the accelerometer, expressed in g's (9.81 m/s^2)

All inertial values are referred to the **body reference fram**. Check the
Argonaut/Medea documentation for further details.

Example of IMU file:

```csv
#GPSWEEK GPSTOW MAGX(uT) MAGY(uT) MAGZ(uT) GYRX(º/s) GYRY(º/s) GYR(º/s) ACCX(g) ACCY(g) ACCZ(g)
1990  210938.42492403     -8.400    56.550   -33.600    -2.305    -0.580     0.641    -0.007     0.053    -0.983
1990  210938.43499108     -9.000    55.800   -31.200    -2.290    -0.641     0.626    -0.015     0.060    -0.980
1990  210938.44496808     -7.650    53.700   -33.150    -2.275    -0.702     0.626    -0.010     0.053    -0.985
```

### Argonaut CAM file

In addition, Argonaut/Medea receivers store any time event that has been
triggered during the data recording campaign. Converting a file that contains
time (cam) events will result in the generation of a file with 2 columns:
(1) the GPS week and (2) the seconds within the GPS week when the time event
took place.

The file has as many rows as events detected by the receiver and the
**time tag is synchronized** to the time scale provided by the GNSS receiver.

If no cam events have been detected, no file will be generated.

Example of CAM (time event) file:

```csv
1990  211188.79867494
1990  211193.86766694
1990  211198.69297889
1990  211201.69084889
1990  211374.67710689
1990  211377.81912194
1990  211380.62477889
```
