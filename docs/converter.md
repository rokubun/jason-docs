# GNSS converter

If you own an Argonaut or Medea receiver you are probably wondering how to
convert the `.rok` files into something else, or how to extract both the
IMU data as well as the time events (if present in the file). Jason provides,
free of charge, a converter that does that.

First of all login to the service and head towards the **GNSS converter** 
(at the top of the page). You should see the following page:

![GNSS converter for Argonaut data](images/howto_conversor.png "GNSS converter for Argonaut data")

Simply drag and drop the file you want to process in the `Raw file`
box and press convert. Once the process is finished, press `Download zip` to 
fetch the data. Assuming that the you uploaded a file named `<input_file>`, you
should see the following files:

- `<input_file>.obs`: The Rinex file (version 3.03) with the GNSS raw measurements recorded by the receiver
- `<input_file>.obs_imu.log`: A columnar file with the IMU data, time tagged in GPS time. See the complete format description [here](#argonaut-imu-file).
- `<input_file>.obs_cam.log`: A columnar file with the event data (e.g. camera event data). See the complete format description [here](#argonaut-cam-file).

Actually, if you have a receiver that ships a ublox receiver, not necessarily
our own, you can still use the tool to convert to Rinex file. However we will
always deny you can do it ;P

## Converted files

This section includes a description of the files delivered by the GNSS converter

### Argonaut GNSS file

Rokubun's Argonaut/Medea receivers store GNSS in Ublox format. The output of the GNSS converter in terms of GNSS measurements data will be the equivalent RINEX 3.03 file as follows:

```txt
     3.03           OBSERVATION DATA    M (MIXED)           RINEX VERSION / TYPE
Rokubun core        rokubun             2019-08-12 15:43:35 PGM / RUN BY / DATE
UNKN                                                        MARKER NAME
unknown             unknown                                 OBSERVER / AGENCY
unknown             unknown             unknown             REC # / TYPE / VERS
unknown             unknown                                 ANT # / TYPE
        0.0000        0.0000        0.0000                  APPROX POSITION XYZ
        0.0000        0.0000        0.0000                  ANTENNA: DELTA H/E/N
  2019    06    05    01    52   03.7652649                 TIME OF FIRST OBS
G    4 C1C L1C D1C S1C                                      SYS / # / OBS TYPES
R    4 C1C L1C D1C S1C                                      SYS / # / OBS TYPES
E    4 C1C L1C D1C S1C                                      SYS / # / OBS TYPES
                                                            END OF HEADER
> 2019 06 05 01 52 20.2019999  0  6
G05  21643026.31606 113734869.95806     -2084.85906        40.00006
G13  20940404.71107 110042563.43007       650.48707        45.00007
G15  21819537.83307 114662444.00207      2552.08207        46.00007
G29  22272808.61807 117044397.73607     -2139.16707        45.00007
G30  24262711.51305 127501402.06305      -245.06005        34.00005
E13  24476988.50208 128627441.38908       970.55808        49.00008
```

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

All inertial values are referred to the **body reference frame**. Check the
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
triggered during the data recording campaign by means of a hot-shoe mounted
on a photogrammetry SLR camera or [MicaSense](http://www.micasense.com).
Converting a file that contains time (cam) events will result in the generation
of a file with 2 columns: (1) the GPS week and (2) the seconds within the GPS
week when the time event took place.

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
