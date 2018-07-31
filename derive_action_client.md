```python
import rospy
import actionlib

import armlib
"""
armlib:
  {
    'kinova': {
      'action_msg': KinovaActionMsg,
      'get_goal': function (target) => KinovaGoalMsg,
      'transition_handler': function (goal_handler) => {...},
      'feedback_handler': function (goal_handler, feedback) => {...},
      'timeout': 5
     },
     ...
  }
"""

"""
This is the entry point to the entire code
"""
hardware_type = 'kinova'

target = {
  coord: [0,0,1],
  speed: 3
  }

rospy.init_node('arm_action_client')

client = actionlib.SimpleActionClient('arm_action', armlib[hardware_type]['action_msg'])

client.wait_for_server()

client.send_goal(armlib[hardware_type]['get_goal'](config), 
                  armlib[hardware_type]['transition_handler'], 
                  armlib[hardware_type]['feedback_handler'])

client.wait_for_result(rospy.Duration.from_sec(armlib[hardware_type]['get_goal'][tmieout]))
```
