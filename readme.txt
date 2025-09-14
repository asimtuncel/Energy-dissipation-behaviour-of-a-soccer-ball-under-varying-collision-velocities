

###  The coefficient of restitution is often represented by a single value, describing the energy lost during an impact 
However, an impact is a continuous process, and energy loss occurs throughout this process. 
Therefore, to better understand how energy is distributed during ball-wall collisions, 
We developed a method to analyse displacement data from high-speed video recordings 
This approach allows us to calculate how the ball’s structural behaviour changes under different impact velocities 
and to determine the energy distribution during the entire collision

# A ball with identical structural properties was projected against a flat wall at four different velocities using a ball-throwing machine
# The impacts were recorded with a high-speed camera operating at 6000 frames per second
# Camera settings: shutter speed = 1/10000, image resolution = 512 × 768 pixels
# The videos were converted to JPEG format using the Photron Fastcam Viewer software (PFV4), and separate folders were created for each velocity condition

#### The folder for each inbound velocity condition ###
# Inbound_velocity1, Inbound_velocity2, Inbound_velocity3 and Inbound_velocity4
# The image data were given by .mp4 format in rthe elated folder


### In order to digitisation of images, "image_processing.py" code was used ###

# The images are digitised when you enter the file path in the code "in image_processing.py"
# All frames from each trial were processed.
# The ball’s geometric center was detected using the HoughCircle command in OpenCV
# The minimum and maximum ball diameters (in pixels) were provided as input parameters
# As a result, pixel-based displacement data were extracted for each impact

	### Please follow the following instructions for data processing

	1. Run the "image_processing.py"
	# Reads the images in the folder containing video images (e.g: 4.1, 4.2, etc.)
	# Open "image_processing.py", navigate to line 14, and specify the file path to read images from the folder named "images".
	# Go to line 15 and change the file name
	# Go to line 40 and 41, set the minimum and maximum diameter of the ball
	# Outputs "...digi.txt" file containing 2D coordinates of the geometric centre and boundaries of the ball 

### Data Filtering ###

To reduce noise in the displacement data, a filtering program was implemented in Python.
A Butterworth low-pass filter with a cutoff frequency of 0.07 Hz was applied.
The cutoff frequency was visually verified to ensure that collision-related signals were preserved.

	### Please follow the following instructions for data filtering
	2. Run "filtering_program_butterworth.py"
	# Reads "...digi.txt" file
	# Apply Butterworth filter
	# Outputs "...filtre.txt" file containing filtered 2D coordinates of the geometric centre and boundaries of the ball 

### Conversion to Metric System ###
To convert filtered pixel data into the metric system, I developed a custom program using Python. 
The conversion was accomplished utilising the Affine Transformation method. For this process, 
We used the pixel coordinates and metric coordinates from the calibration image employed during the testing phase. 
The pixel coordinates of the calibration image were documented in the "calib_im.txt" file, while the metric coordinates of the calibration image were given inside the program
This approach ensured that the data was accessible for calculations at all velocities.


	### Please follow the following instructions for metric transformation
	3.1. Open "metric_transformation.py", go to line 107. Change "ad" accordingly (e.g: 4.1, 4.2, etc.)
	3.2. Run the "metric_transformation_AFFIN.py"
	# Reads "calib_im.txt" that contains 2D coordinates of the calibration image
	# Reads "...filtre.txt" file
	# Performs affine transformation and returns 2D coordinates in meters ("...metrik.txt")

### Calculate the impact parameter for indentation and contact surface area ###

From the metric data, the following parameters were calculated
Ball indentation during impact and Contact surface area

	### Please follow the instructions to calculate the indentation and contact surface area
	4. Run "calculate_collision_parameters.py"
	# Reads "...metrik.txt" file
	# Calculates indentation amount and contact surface area
	# Outputs "...metrik_hesap.txt"
	

### Calculate to collision dynamics
The ball's collision parameters were calculated using the displacement coordinates made available by the processes mentioned earlier. 
These parameters included the ball's indentation during the impact and the area of the contact surface.
After calculating the ball's impact indentation and contact surface area, 
the ball's displacement data (velocity, acceleration, mass, reaction forces, and contact surface area) were calculated.
This provided the parameters necessary to calculate the energy distribution during the collision.

# Velocity, acceleration, reaction forces, and time-dependent contact area
# These parameters were required to describe energy distribution throughout the collision

	
	### Please follow the instructions to calculate collision parameters
	5.1. Open "calculate_vel_acc_force_k_c.py", go to line 16. Change "ball" accordingly (e.g: 4.1, 4.2, etc.)
	5.2. Run "calculate_vel_acc_force_k_c.py"
	# Reads "...metrik_hesap.txt"
	# Calculates ball velocity, acceleration, effective mass, impact force, spring and damping parameters
	# Outputs "...velocity.txt", "...acceleration.txt", "...impact_force.txt", "...spring_damper.txt" files


### Validation of Results ###

To determine the accuracy of the data obtained through image processing, a mass-spring-damper model was created using the ball's inbound velocity 
and the calculated spring and damper coefficients. 
Numerical integration was performed using the Rungge-Kutta method, and the model's velocity and indentation during the impact were calculated 
These calculated values ​​were compared with the data obtained through image processing analysis to verify the accuracy of the data obtained 
Root mean square error and percentage root mean square error were calculated for this purpose. 
The comparison determined that the indentation was less than 5% and the velocity was less than 7.38% in error


# A mass-spring-damper model was developed using the ball’s pre-impact velocity and estimated stiffness and damping coefficients
# Numerical integration was performed with the Runge-Kutta method
# Model predictions of indentation and velocity were compared with image-processing results
# Error rates: indentation < 5%, velocity < 7.38%

	This confirmed the reliability of the image-processing approach
	6.1. Open "perform_rungekutta.py", go to line 16. Change "ad" accordingly (e.g: 4.1, 4.2, etc.)
	6.2. Run "perform_rungekutta.py"
	# Reads "...metrik_hesap.txt", "...velocity.txt", "...acceleration.txt"
	# Solves differential equation using Runge-Kutta method
	# Performs statistical analyses, compares experimental and simulation results
	# Prints the results in Python Console
	# Outputs "...runge_kutta_oututs.txt"


### Energy Distribution Calculation ###
To determine the energy distribution during the collision, the work done by the ball and the amount of elastic potential energy must be determined 
Using the work done by the ball and the elastic potential energy data during the collision, a formula was developed to calculate 
the ball's energy loss at each instant during the collision using a custom program written in Python.

# The ball’s mechanical work and elastic potential energy during impact were calculated
# Using the developed formula, the energy loss at each instant of the collision was determined
# These calculations were performed using a custom Python program
	

	### Please follow the following instructions
	7.1. Open "calculate_eddc.py", go to line 10. Change "ad" accordingly (e.g: 4.1, 4.2, etc.)
	7.2. Go to line 18 and determine how many additional lines are needed to obtain the force values up to the maximum indentation, based on a visual inspection of the hysteresis graph.
	7.3. Run "calculate_eddc.py"
	# Reads "...impact_force.txt", "...metrik_hesap.txt", "...spring_damper.txt"
	# Calculates energy dissipation during the collision, elastic potential energy and, work
	# Outputs "...EPE_CP.txt", "...EPE_RP.txt", "...WORK_CP.txt", "...WORK_RP.txt", "..._cor_compr_phase.txt", "..._cor_res_phase.txt" 
	

### Mean Energy Dissipation During the Collision ###
#  Each mean value was calculated for comparison of the results according to velocity conditions
	
	### Please follow the following instructions
	8.1. Open "calculate_mean_cor.py", go to line 12. Change "name" accordingly (e.g, 4, 5, etc.)
	8.2. Run "calculate_cor_calculation.py" 
	# Reads "..._cor_compr_phase.txt", "..._cor_res_phase.txt" 
	# Calculates mean coefficient of restitution for selected trials
	# Outputs "...mean_comp_cor.txt", "...mean_res_cor.txt", "...mean_cor_gir.txt"

### Mean EPE results During the Collision ###
#  Each mean value was calculated for comparison of the results according to velocity conditions

	### Please follow the following instructions
	9.1. Open "calculate_mean_epe.py", go to line 12. Change "name" accordingly (e.g: 4, 5, etc.)
	9.2. Run "calculate_mean_epe.py" 
	# Reads "..._EPE_CP.txt", "..._EPE_RP.txt" 
	# Calculates mean elastic potential energy for selected trials
	# Outputs "...mean_comp_epe.txt", "...mean_res_epe.txt"

### Mean Work results During the Collision ###
#  Each mean value was calculated for comparison of the results according to velocity conditions

	### Please follow the following instructions
	10.1. Open "calculate_mean_work.py", go to line 12. Change "name" accordingly (e.g: 4, 5, etc.)
	10.2. Run "calculate_mean_work.py" 
	# Reads "..._WORK_CP.txt", "..._WORK_RP.txt" 
	# Calculates mean work for selected trials
	# Outputs "...mean_comp_work.txt", "...mean_res_work.txt"


### Mean Impact Force results During the Collision ###
#  Each mean value was calculated for comparison of the results according to velocity conditions

	### Please follow the following instructions
	11.1. Open "calculate_mean_force.py", go to line 12. Change "name" accordingly (e.g: 4, 5, etc.)
	11.2. Run "calculate_mean_force.py" 
	# Reads "...impact_force.txt"
	# Calculates mean impact force for selected trials
	# Outputs "...mean_comp_force.txt", "...mean_res_force.txt"

### Visualisation of data

	### Please follow the instructions for the visualisation
	12.1. Open "plot_work.py", go to line 11. Change "ball_name" accordingly (e.g: 4., 5., etc.)
	12.2. Run "plot_work.py" 
	# Reads "..._WORK_CP.txt", "..._WORK_RP.txt", "...mean_comp_work.txt", "...mean_res_work.txt"
	# Plots the work results

	13.1. Open "plot_epe.py", go to line 11. Change "ball_name" accordingly (e.g: 4., 5., etc.)
	13.2. Run "plot_epe.py" 
	# Reads "..._EPE_CP.txt", "..._EPE_RP.txt", "...mean_comp_epe.txt", "...mean_res_epe.txt"
	# Plots the elastic potential energy results

	14. Run "plot_ind_vel.py" 
	# Reads "..._runge_kutta_outputs.txt"
	# Plots indentations and velocities




