# Rectangular Bar Magnet Magnetic Flux Field Finder

Function written in Java.

## Returns:
The magnetic Flux (B field) Vector (in the form of a 3 element array, that represents the x,y,z components of the vector) with units Teslas, from a rectangular bar magnet. The vector is of the B field at a specific x,y,z coordinate relative the the magnet (coordinate system origin is at the center of the magnet)

![Bfield_at_xyz](https://github.com/PopeyedLocket/Rect-Bar-mag-B-Field-Finder/blob/master/images/Bfield_at_xyz_image.jpg?raw=true "B filed at (x,y,z)" width="200" height="400")

## Arguments:<br />
- x, y, z (type: double) are the coordinates of the point at which the B field is to be found in meters<br />
- mx, my, mz (type: double) are the width, height, and depth of the rectangular bar magnet in meters<br />
- mag_dir (type: double) is the vector of the magnetization of the magnet in A/m,<br />
  * it is confined to the y direction in A/m<br />
  * positive inputs represent a magnetization in the positive y direction<br />
    * i.e. the north end of the magnet is in the positive y direction<br />
  * negative inputs represent a magnetization in the negative y direction<br />
    * i.e. the south end of the magnet is in the positive y direction<br />
    
## Sources:
The equations used to calculate the magnetic field were found from journal 1 by Vlatko Cingoski and Hideo Yamashita, provided here in the Sources folder.
