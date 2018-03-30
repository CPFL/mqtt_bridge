# mqtt_bridge for AMS-Autoware connection

This MQTT_bridge has been improved to connect AMS and Autoware.
The topic name can be changed dynamically by roslaunch argument.

## How to setup

Install necessary packages as below.

https://github.com/groove-x/mqtt_bridge


Set up Autoware and AMS as below.

https://github.com/CPFL/Autoware

https://github.com/CPFL/AMS

Build as below.

```bash
cp -r mqtt_bridge ${Autoware_path}/Autoware/ros/src/util/package/
chmod +x ${Autoware_path}/Autoware/ros/src/util/package/mqtt_bridge/script/mqtt_bridge_node.py
cd ${Autoware_path}/Autoware/ros/
catkin_make --pkg mqtt_bridge
rosdep install mqtt_bridge
```


##example

Write the character string to replace with enclosed in {}.
```yaml
factory: mqtt_bridge.bridge:RosToMqttBridge
msg_type: std_msg.msg:Int32 
topic_from: /test{str1}
topic_to: {topic1}
```

Execute launch file like below.

```bash
roslaunch Autoware_AMS_bridge.launch replace_strings:="{'str1':'1','topic1':'/test2'}"
```

The topic to transfer is as follows.

```
topic_from: /test1
topic_to: /test2
```

In case of using Autoware unique message, execute below before roslaunch

```bash
source ${Autoware_path}/Autoware/ros/devel/setup.bash
```