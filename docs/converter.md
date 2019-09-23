# GNSS converter

If you own an Argonaut or Medea receiver you are probably wondering how to
convert the `.rok` files into something else, or how to extract both the
IMU data as well as the time events (if present in the file). Jason provides,
free of charge, a converter that does that.

First of all login to the service and head towards the **GNSS converter** 
(at the top of the page). You should see the following page:

![GNSS converter for Argonaut data](images/howto_conversor.png "GNSS converter for Argonaut data")

Once there, simply drag and drop the file you want to process in the `Raw file`
box and press convert. Once the process is finished press `Download zip` to 
fetch the data. Assuming that the you uploaded a file named `<input_file>`, you
should see the following files:

- `<input_file>.obs`: The Rinex file (version 3.03) with the GNSS raw measurements recorded by the receiver
- `<input_file>.obs_imu.log`: A columnar file with the IMU data, time tagged in GPS time. See the complete format description in the [format page](../manual#argonaut-imu-file).
- `<input_file>.obs_cam.log`: A columnar file with the event data (e.g. camera event data). See the complete format description in the [format page](../manual#argonaut-cam-file).

Actually, if you have a receiver that ships a ublox receiver, not necessarily
our own, you can still use the tool to convert to Rinex file. However we will
always deny you can do it ;P
