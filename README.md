# Big data nautical charts that are safe for shipping

The [Danish Geodata Agency](http://www.gst.dk/English/) produce data and maps that are used for navigation in danish territorial waters including Greenland. Having highly accurate digital map data for a coastline as vast as the one surrounding Greenland, is a challenge. To make it possible to work with the data, so-called simplification algorithms are often used, which transforms a high resolution geometric object (such as a coastline) into a low-resolution geometric object.

When producing maps for navigation, it is important that geographic features such as a small island are not "simplified away". Although small in area, such a small rocky island may still cause a ship wreck! Another example could be a small peninsula that although small protrudes out into the ocean near an important shipping line.

![Ship wreck](http://upload.wikimedia.org/wikipedia/commons/thumb/c/cc/8_-_AmStar_7.JPG/360px-8_-_AmStar_7.JPG)

That map data is often simplified can be seen on the following [two images from Google Maps](https://maps.google.com/?ll=64.016452,-51.627846&spn=0.098822,0.363579&t=h&z=12) (try opening the link and flipping between "map" and "satellite" view). They are of the same area on the coast of Greenland.

![Satellite image of Greenland](http://i.imm.io/SdqG.png)  ![Map image of Greenland](http://i.imm.io/SdqU.png) 

As can be seen, it would be unwise to use Google Maps as a nautical chart, which is not what Google Maps is designed for.

For an introduction to simplification algorithms, see the Wikipedia article on the [Ramer-Douglas-Peucker algorithm](http://en.wikipedia.org/wiki/Ramer%E2%80%93Douglas%E2%80%93Peucker_algorithm). It should be noted that Ramer-Douglas-Peucker would be a very bad choice for a simplification algorithm for coastlines, as it would most likely remove small islands and peninsulas!

**Example of line simplification**:

![Example of line simplification](http://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Douglas-Peucker_animated.gif/220px-Douglas-Peucker_animated.gif)

## Project description

In this project you will design a simplification algorithm that reduces the number of points needed to represent a coastline, while maintaining safety for shipping if the coastline data is used to produce a nautical chart.

You will think about the guarantees your algorithm offers:

* Does it only add land mass?
* Does it only move the coastline by a certain amount?

An simple algorithm that would produce a "safe" shipping map, would be to simply compute the minimum bounding rectangle around all (closed circuit) coastlines, but in the case of Greenland, that would make it impossible to navigate the fjords. A good algorithm produces output with the following properties:

* Generally the output has high fidelity compared to the input
* Generally the output is significantly smaller in size than the input
* A shipping route that would result in a ship wreck for the input, would also result in a ship wreck for the output
* A coordinate that is reachable by ship for the input, is also be reachable by ship in the output (by a margin of *x* meters)

Data will be provided by [Danish Geodata Agency](http://www.gst.dk/English/) or by OpenStreetMap if that is easier.

The [OpenStreetMap data for Greenland](http://download.cloudmade.com/americas/northern_america/greenland#downloads_breadcrumbs) is free to download. It has the following properties:

* 21K linestrings total
* 572K points total
* 3K non-rings (propably mainland coastline segments). Average 82 points. Max 530 points
* 18K rings (propably islands). Average 15 points. Max 1248 points

Running Ramer-Douglas-Peucker on the entire dataset (run independently on each linestring) reduces the number of points (depending on the algorithm *tolerance* argument). All linestring have been projected from lat-lon to the [GR96 / UTM zone 29N](http://georepository.com/crs_3189/GR96-UTM-zone-29N.html) projection:

<table>
	<tr>
		<th>Tolerance in meters</th>
		<th>Reduction in points</th>
		<th># Points</th>
		<th>Average points per linestring</th>
		<th>Minimum points for linestring</th>		
	</tr>
	<tr>
		<td>0m</td>
		<td>0%</td>
		<td>572K</td>
		<td>26</td>
		<td>2</td>
	</tr>
	<tr>
		<td>1m</td>
		<td>0.8%</td>
		<td>567K</td>
		<td>26</td>
		<td>2</td>
	</tr>
	<tr>
		<td>25m</td>
		<td>11%</td>
		<td>508K</td>
		<td>23</td>
		<td>1</td>
	</tr>
	<tr>
		<td>100m</td>
		<td>68%</td>
		<td>128K</td>
		<td>8</td>
		<td>1</td>
	</tr>
	<tr>
		<td>500m</td>
		<td>90%</td>
		<td>56K</td>
		<td>3</td>
		<td>1</td>
	</tr>
</table>

The problem with using Ramer-Douglas-Peucker is that e.g. with 25m tolerance many small islands collapse to points:

<table>
	<tr>
		<th>Points before</th>
		<th>Points after</th>
		<th>Island area before</th>
	</tr>
	<tr>
		<td>4</td>
		<td>1</td>
		<td>112 m2</td>		
	</tr>
	<tr>
		<td>14</td>
		<td>1</td>
		<td>145 m2</td>		
	</tr>
	<tr>
		<td>9</td>
		<td>1</td>
		<td>78 m2</td>		
	</tr>
	<tr>
		<td>9</td>
		<td>1</td>
		<td>56 m2</td>		
	</tr>
	<tr>
		<td>8</td>
		<td>1</td>
		<td>67 m2</td>		
	</tr>
	<tr>
		<td>10</td>
		<td>1</td>
		<td>102 m2</td>		
	</tr>
</table>

You do not want small reefs disappearing on a nautical chart!

If you are interested in doing this project, send an email to kostas@diku.dk.

* [Read more about the nautical charts produced by the agency](http://www.gst.dk/English/NauticalChartsandNavigation/)


## External partner

The project is done in collaboration with the [Danish Geodata Agency](http://www.gst.dk/English/)


