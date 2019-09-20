# Usage examples

This section includes several usage examples that cover most of the use cases
that Jason could support.

## Rover file

Input rover file in Rinex 3.03 format. base will be looked for automatically

The simplest 

## Rover and base files

In this case

## Rover file with events

Argonaut receiver contains time events. 


## Static receiver, RTCM 3 format

The use case for this example is in the event that you deploy a base station
so that it transmits the data via NTRIP to an NTRIP caster. Rover receivers
can then connect to this caster but need the precise coordinates of this base
station.

Once the base station is serving data to the NTRIP caster, the operator can
record data into `rtcm3` format using e.g. [rtklib](http://www.rtklib.com)'s `str2str` tool.
After you log in into Jason, send the data, as shown in the following figure
(for a data file `bcln0.rtcm3`)

![Process an RTCM3 file in static mode](images/howto_rtcm3_static.png "Process an RTCM3 file in static mode")

One point to take into account is the fact that the file conversion within
Jason does not allow the user to specify the approximate date of the file.
Therefore, unless the RTCM3 file is recent (within the same GPS week), the
RTCM3 file will not he processed. Therefore, the recommended approach would
be to convert the rtcm3 file into Rinex and then upload it to the service.
If you use `rtklib`'s `convbin` tool, you can launch the command:

```bash
convbin -r rtcm3 -v 3.03 -f 3 -scan -o bcln0.rinex bcln0.rtcm3
```

Then upload the file `bcln0.rinex` to Jason.

## Argonaut/Medea file conversion

If you own an Argonaut or Medea receiver you are probably wondering how to
convert the `.rok` files into something else, or how to extract both the
IMU data as well as the time events (if present in the file). Jason provides,
free of charge, a conversor that does that.

First of all login to the service and head towards the **GNSS converter** 
(at the top of the page). You should see the following page:

![GNSS conversor for Argonaut data](images/howto_conversor.png "GNSS conversor for Argonaut data")

Once there, simply drag and drop the file you want to process in the `Raw file`
box and press convert. Once the process is finished press `Download zip` to 
fetch the data. Assuming that the you uploaded a file named `<input_file>`, you
should see the following files:

- `<input_file>.obs`: The Rinex file (version 3.03) with the GNSS raw measurements recorded by the receiver
- `<input_file>.obs_imu.log`: A columnar file with the IMU data, time tagged in GPS time. See the complete format description in the [format page](../file_formats#argonaut-imu-file).
- `<input_file>.obs_cam.log`: A columnar file with the event data (e.g. camera event data). See the complete format description in the [format page](../file_formats#argonaut-cam-file).

Once 

Actually, if you have a receiver that ships a Ublox receiver, not necessarily
our own, you can still use the tool to convert to Rinex file. However we will
always deny you can do it.

### Usage of external tools

Because 

If you use Docker, feel free to use our dockerized container with a bundle of
GNSS processing tools.

