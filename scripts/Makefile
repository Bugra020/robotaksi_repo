CARLA_SERVER=~/carla/Dist/CARLA_Shipping_0.9.15-262-g8f7e40f3c-dirty/LinuxNoEditor/CarlaUE4.sh
ROS_BRIDGE=ros2 launch carla_ros_bridge carla_ros_bridge.launch.py
LIDAR_PUBLISHER=ros2 run carla_lidar_publisher lidar_publisher
STATIC_TF_PUBLISHER=ros2 run carla_lidar_publisher static_tf_publisher
DYNAMIC_TF_PUBLISHER=ros2 run carla_lidar_publisher dynamic_tf_publisher

run: kill
	@echo "Starting CARLA Simulator..."
	@(${CARLA_SERVER} -RenderOffScreen > /dev/null 2>&1 &)
	@sleep 15

	@echo "Starting ROS2 Bridge..."
	@(${ROS_BRIDGE} > /dev/null 2>&1 &)
	@sleep 5

	@echo "Running the static tf publisher..."
	@(${STATIC_TF_PUBLISHER} > /dev/null 2>&1 &)
	@sleep 1
	
	@echo "Running the dynamic tf publisher..."
	@(${DYNAMIC_TF_PUBLISHER} > /dev/null 2>&1 &)
	@sleep 1

	@echo "Running the Spawn Script..."
	@(${LIDAR_PUBLISHER})
 
kill:
	@echo "Stopping CARLA, ROS bridge, static_tf_publisher and dynamic_tf_publisher..."
	@-pkill -f CarlaUE4 > /dev/null 2>&1 || true
	@-pkill -f carla_ros_bridge > /dev/null 2>&1 || true
	@-pkill -f static_tf_publisher > /dev/null 2>&1 || true
	@-pkill -f dynamic_tf_publisher > /dev/null 2>&1 || true

restart: kill run
