```python
import time

class ActionClientAdapter(object):
  def __init__(self, type, payload):
    """
    type: a string represent which action server to connect
    payload: a dict specifying information needed to connect, for example:
      {
        node_name: "my_action_client",
        namespace: "my_action",
        action_msg: MyAction,
        goal_msg: MyGoal,
        deadline: 1e5,
        timeout: rospy.Duration(5.0),
        feedback_handler: function (goal_handler, feedback) => {...},
        result_handler: function (goal_handler) => {...},
      }
    """
    self.type = type
    self.payload = payload
    self.client = None
    
  def connect(self):
    rospy.init_node(self.payload['node_name']);
    self.client = actionlib.SimpleActionClient(self.payload['namespace'], self.payload['action_msg'])
    client.wait_for_server(self.payload['timeout'])
    
  def feedback_handler(self, goal_handler, feedback):
    self.payload['feedback_handler'](goal_handler, feedback)
    
  def result_handler(self, goal_handler):
    self.payload['result_handler'](goal_handler)
    
  def execute(self):
    self.client.send_goal(goal=self.payload['goal_msg'](), transition_cb=self.feedback_handler, feedback_cb=self.result_handler)
```
