# Rect Bar Mag B Field Finder

Written in Java.

returns: B field in Teslas from a magnet at the coordinates of the point specified (coordinate origin is at the center of the magnet)

arguments:
	 x, y, z are the coordinates of the point at which the B field is found in meters
	 mx, my, mz are the width, height, and depth of the rectangular bar magnet in meters
	 mag_dir is the vector of the magnetization of the magnet in A/m,
	  		it is confined to the y direction in A/m
	  		positive inputs represent a magnetization in the positive y direction
	  			i.e. the position of the north end of the magnet has a positive y value 
	  		negative inputs represent a magnetization in the negative y direction
	  	 		i.e. the position of the north end of the magnet has a negative y value
