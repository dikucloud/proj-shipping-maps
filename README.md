# Big data navigation maps that are safe for shipping

The [Danish Geodata Agency](http://www.gst.dk/English/) produce data and maps that are used in naval navigation in danish territorial waters including Greenland. Having highly accurate digital map data for a coastline as vast as the one surrounding Greenland, is a challenge. To make it possible to work with the data, so-called simplification algorithms are used, which transforms a high resolution geometric object (such as a coastline) into a low-resolution geometric object.

When producing maps for navigation, it is important that geographic features such as a small island are not "simplified away". Although small in area, such a small rocky island may still cause a ship wreck! Another example could be a small peninsula that although small protrudes out into the ocean crossing an important shipping line.

That map data is often simplified can be seen on the following two images from Google Maps. They are of the same area on the [coast of Greenland](https://maps.google.com/?ll=64.078279,-51.448288&spn=0.020974,0.076904&t=m&z=14).

![Satellite image of Greenland](http://i.imm.io/S8fP.png)  ![Map image of Greenland](http://i.imm.io/S8fe.png) 

As can be seen, it would be unwise to navigate a ship according to the map images of Greenland from Google Maps.

For an introduction to simplification algorithms, see the Wikipedia article on the [Ramer-Douglas-Peucker algorithm](http://en.wikipedia.org/wiki/Ramer%E2%80%93Douglas%E2%80%93Peucker_algorithm)

**Example of line simplification**:

![Example of line simplification](http://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Douglas-Peucker_animated.gif/220px-Douglas-Peucker_animated.gif)

## Project description

In this project you will produce a geometric simplification algorithm that reduces the size of a geographical dataset for a coastline, while maintaining the safety for shipping.

* Automatically remove points from a coastline object (including islands) to reduce size of data
* Resulting coastline must still be safe for shipping, without adding large amounts of land area (e.g. the bounding rectangle for greenland would be a "safe" coastline, but would make it impossible to navigate the fjords).


Data will be provided by [GST](http://www.gst.dk/English/) for the project (data is *confidential* and must not be used outside the project).

If you are interested in doing this project, send an email to kostas@diku.dk.

## External partner

The project is done in collaboration with the [Danish Geodata Agency](http://www.gst.dk/English/)


