# Why the file I uploaded is not processing within JASON engine?

JASON engine requires GNSS raw data to be able to extract the satellite ranging information in which precise positioning is based, this means that your rover receiver must be correctly configured or otherwise JASON will not be able to find the minimum required information.

For example, if you want to upload u-blox data you must ensure that your file, at the very least, contains UBX-RXM-RAWX, if you are uploading Septentrio data then you must ensure that your file contains MeasEpoch or Meas3Ranges.

