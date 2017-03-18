package package1;

public class B_field_finder {

	/* returns: B field in Teslas from a magnet at the coordinates of the point specified (coordinate origin is at the center of the magnet)
	 * 
	 * arguments:
	 * x, y, z are the coordinates of the point at which the B field is found in meters
	 * mx, my, mz are the width, height, and depth of the rectangular bar magnet in meters
	 * mag_dir is the vector of the magnetization of the magnet in A/m,
	 * 		it is confined to the y direction in A/m
	 * 		positive inputs represent a magnetization in the positive y direction
	 * 			i.e. the position of the north end of the magnet has a positive y value 
	 * 		negative inputs represent a magnetization in the negative y direction
	 * 	 		i.e. the position of the north end of the magnet has a negative y value
	 */
	public double [] Bfield(double x, double y, double z, double mx, double my, double mz, double mag_dir) { 
		
		double   xb = mx/2,      yb = my/2,      zb = mz/2;
		
		double[] M = new double[]{mag_dir,0,0}; // magnetization vector [A/m]
		
		double[] H = new double[3]; // H field
		double[] H_sum = new double[3]; // helper array to find H field
		double[] B = new double[3]; // Magnetic Flux Density [T], btw 1[T] = 1[kg*s^-2*A^-1]
		
		for (int k = 1; k <= 2; k++){
			for (int l = 1; l <= 2; l++) {
				for (int m = 1; m <= 2; m++) {
					H_sum[0] += Math.pow(-1,k+l+m) *
							  (((x+Math.pow(-1,k)*xb)*(z+Math.pow(-1,m)*zb)) /
							  ((Math.abs(x+Math.pow(-1,k)*xb))*(Math.abs(z+Math.pow(-1,m)*zb)))) *
							  Math.atan(
									  ((Math.abs(z+Math.pow(-1,m)*zb))*(y+Math.pow(-1,l)*yb)) /
									  ((Math.abs(x+Math.pow(-1,k)*xb))* Math.sqrt(
											  Math.pow(x+Math.pow(-1,k)*xb,2) +
											  Math.pow(y+Math.pow(-1,l)*yb,2) +
											  Math.pow(z+Math.pow(-1,m)*zb,2)
											  )
									   )
							  );
					H_sum[1] += Math.pow(-1,k+l+m) * 
							  Math.log(
									  z +
									  Math.pow(-1,m)*zb +
									  Math.sqrt(
											  Math.pow(x+Math.pow(-1,k)*xb,2) +
											  Math.pow(y+Math.pow(-1,l)*yb,2) +
											  Math.pow(z+Math.pow(-1,m)*zb,2)
									  )
							  );
					H_sum[2] += Math.pow(-1,k+l+m) * 
							  Math.log(
									  y +
									  Math.pow(-1,l)*yb +
									  Math.sqrt(
											  Math.pow(x+Math.pow(-1,k)*xb,2) +
											  Math.pow(y+Math.pow(-1,l)*yb,2) +
											  Math.pow(z+Math.pow(-1,m)*zb,2)
									  )
							  );
				}
			}
		}
		
		H[0] = -(M[0]/(4*Math.PI))*H_sum[0];
		H[1] = (M[0]/(4*Math.PI))*H_sum[1];
		H[2] = (M[0]/(4*Math.PI))*H_sum[2];
		
		double u0 = 4*Math.PI*Math.pow(10,-7); // magnetic permeability of air [H/m], btw 1[H] = 1[kg*m^2*s^-2*A^-2]
		if (x <= xb && x >= -xb && y <= yb && y >= -yb && z <= zb && z >= -zb) {
			B[0] = u0*(H[0]+M[0]);
			B[1] = u0*(H[1]+M[1]);
			B[2] = u0*(H[2]+M[2]);
		} else {
			B[0] = u0*H[0];
			B[1] = u0*H[1];
			B[2] = u0*H[2];
		}
	return B;
	}
}
