##The image data of the study was separated into different folders due to the upload limit
##It is digitized when you enter the file path in the code in image_processing.py in the codes and data folder

### Codes and data folder###
Please follow the following instructions for data processing

# Reads the images in the folder containing video images (e.g: 4_1, 4_2, etc.)
# Open "image_processing.py", navigate to line 14, and specify the file path to read images from the folder named "images".
# Go to line 15 and change the file name
# Go to line 40 and 41, set the minimum and maximum diameter of the ball
# Outputs "...digi.txt" file containing 2D coordinates of the geometric centre and boundaries of the ball 
1. Run the "image_processing.py"

# Reads "...digi.txt" file
# Apply butterworth filter
# Outputs "...filtre.txt" file containing filtered 2D coordinates of the geometric centre and boundaries of the ball 
2. Run "filtering_program_butterworth.py"

# Reads "calib_im.txt" that contains 2D coordinates of the calibration image
# Reads "...filtre.txt" file
# Performs affine transformation and returns 2D coordinates in meters ("...metrik.txt")
3.1. Open "metric_transformation.py", go to line 107. Change "ad" accordingly (e.g: 4_1, 4_2, etc.)
3.2. Run the "metric_transformation_AFFIN.py"

# Reads "...metrik.txt" file
# Calculates indentation amount and contact surface area
# Outputs "...metrik_hesap.txt"
4. Run "calculate_collision_parameters.py"

# Reads "...metrik_hesap.txt"
# Calculates ball velocity, acceleration, effective mass, impact force, spring and damping parameters
# Outputs "...velocity.txt", "...acceleration.txt", "...impact_force.txt", "...spring_damper.txt" files
5.1. Open "calculate_vel_acc_force_k_c.py", go to line 16. Change "ball" accordingly (e.g: 4_1, 4_2, etc.)
5.2. Run "calculate_vel_acc_force_k_c.py"

# Reads "...metrik_hesap.txt", "...velocity.txt", "...acceleration.txt"
# Solves differential equation using runge-kutta method
# Performs statistical analyses, compares experimental and simulation results
# Prints the results in Python Console
# Outputs "...runge_kutta_oututs.txt"
6.1. Open "perform_rungekutta.py", go to line 16. Change "ad" accordingly (e.g: 4_1, 4_2, etc.)
6.2. Run "perform_rungekutta.py"

# Reads "...impact_force.txt", "...metrik_hesap.txt", "...spring_damper.txt"
# Calculates energy dissipation during the collision, elastic potential energy and, work
# Outputs "...EPE_CP.txt", "...EPE_RP.txt", "...WORK_CP.txt", "...WORK_RP.txt", "..._cor_compr_phase.txt", "..._cor_res_phase.txt" 
7.1. Open "calculate_eddc.py", go to line 10. Change "ad" accordingly (e.g: 4_1, 4_2, etc.)
7.2. Go to line 18 and determine how many additional lines are needed to obtain the force values up to the maximum indentation, based on a visual inspection of the hysteresis graph.
7.3. Run "calculate_eddc.py"
#### 

# Reads "..._cor_compr_phase.txt", "..._cor_res_phase.txt" 
# Calculates mean coefficient of restitution for selected trials
# Outputs "...mean_comp_cor.txt", "...mean_res_cor.txt", "...mean_cor_gir.txt"
8.1. Open "calculate_mean_cor.py", go to line 12. Change "name" accordingly (e.g: 4, 5, etc.)
8.2. Run "calculate_cor_calculation.py" 

# Reads "..._EPE_CP.txt", "..._EPE_RP.txt" 
# Calculates mean elastic potential energy for selected trials
# Outputs "...mean_comp_epe.txt", "...mean_res_epe.txt"
9.1. Open "calculate_mean_epe.py", go to line 12. Change "name" accordingly (e.g: 4, 5, etc.)
9.2. Run "calculate_mean_epe.py" 

# Reads "..._WORK_CP.txt", "..._WORK_RP.txt" 
# Calculates mean work for selected trials
# Outputs "...mean_comp_work.txt", "...mean_res_work.txt"
9.1. Open "calculate_mean_work.py", go to line 12. Change "name" accordingly (e.g: 4, 5, etc.)
9.2. Run "calculate_mean_work.py" 

# Reads "...impact_force.txt"
# Calculates mean impact force for selected trials
# Outputs "...mean_comp_force.txt", "...mean_res_force.txt"
10.1. Open "calculate_mean_force.py", go to line 12. Change "name" accordingly (e.g: 4, 5, etc.)
10.2. Run "calculate_mean_force.py" 

# Reads "..._WORK_CP.txt", "..._WORK_RP.txt", "...mean_comp_work.txt", "...mean_res_work.txt"
# Plots the work results
11.1. Open "plot_work.py", go to line 11. Change "ball_name" accordingly (e.g: 4_, 5_, etc.)
11.2. Run "plot_work.py" 

# Reads "..._EPE_CP.txt", "..._EPE_RP.txt", "...mean_comp_epe.txt", "...mean_res_epe.txt"
# Plots the elastic potential energy results
12.1. Open "plot_epe.py", go to line 11. Change "ball_name" accordingly (e.g: 4_, 5_, etc.)
12.2. Run "plot_epe.py" 

# Reads "..._runge_kutta_outputs.txt"
# Plots indentations and velocities
13. Run "plot_ind_vel.py" 



