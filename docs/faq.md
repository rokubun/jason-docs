# Frequently Asked Questions

Do you have a question not listed here? [Drop us a line!](mailto:info@rokubun.cat?subject=[Jason doc] faq request)

> How accurate is the solution I've got with Jason?

You can find the error estimate in the error columns of the [position files
delivered within the ZIP bundle](../manual#position-files-csv).

Note however that this error estimate comes from the post-fit covariance values
delivered by the navigation filter. These values are a basic metric
to assess the quality of the solution but are formal errors and, as such, do not represent
the actual error of the solution. To obtain an actual error of the solution an
external reference for comparison is required.

> I cannot display NMEA files? why is that?

Jason is designed to process raw GNSS measurements to obtain the position
(NMEA format is used to represent positions, no GNSS raw measurements).

If you are trying to plot the contents of a NMEA file into a map such as
e.g. Google Earth, we recommend you to convert NMEA to KML (using external
tools such as e.g. rtklib's `pos2kml`).
