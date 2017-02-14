# MAVLink-Proximity
ArduPilot Copter supports object avoidance using  any sensor capable of providing distances using the MAVLink DISTANCE_SENSOR message. The repository stakes source code and describing, how the object avoidance feature works and how “proximity sensors” should provide data into ArduPilot. 
# Providing Distance Sensor messages to ArduPilot
For developers of new “proximity” sensors (i.e. sensors that can somehow provide the distance to nearby objects) the easiest method to get your distance measurements into ardupilot is to send DISTANCE_SENSOR message for each direction the sensor is capable of. The system id of the message should match the system id of the vehicle (default is “1” but can be changed using the SYSID_THISMAV parameter). The component id can be anything but MAV_COMP_ID_PATHPLANNER (195) or MAV_COMP_ID_PERIPHERAL (158) are probably good choices.

These messages should be sent at between 10hz and 50hz (the faster the better). The fields should be filled in as shown below:

time_boost_ms : 0 (ignored)
min_distance : the minimum distance that the sensor can measure in centimeters (i.e. 100 = 1m). This number should generally not change and should be the same regardless of the orientation field.
max_distance : the maximum distance that the sensor can measure in centimeters (i.e. 1500 = 15m). This number should generally not change and should be the same regardless of the orientation field.
current_distance : the shortest distance in cm to the object
type : 0 (ignored)
id : 0 (ignored)
orientation : 0 to 7 (0=forward, each increment is 45degrees more in clockwise direction), 24 (upwards) or 25 (downwards). search for MAV_SENSOR_ORIENTATION on the mavlink/common page.
covariance : 0 (ignored)
