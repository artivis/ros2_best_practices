# Launch

Find the doc [here](https://index.ros.org/doc/ros2/Tutorials/Launch-system/).

Find the [presentation at ROSCon 2018](https://roscon.ros.org/2018/presentations/ROSCon2018_launch.pdf).

### Passing launch prefix

```python
def generate_launch_description():

    ld = LaunchDescription(...)

    ld.add_action(launch.actions.SetLaunchConfiguration('launch-prefix', 'valgrind'))
```

### Launching a CLI publisher
```python
import sys

from launch import LaunchDescription
from launch.actions.execute_process import ExecuteProcess


def generate_launch_description():
    # Necessary to get real-time stdout from python processes:
    proc_env = os.environ.copy()
    proc_env['PYTHONUNBUFFERED'] = '1'

    publisher = ExecuteProcess(
        cmd=['ros2 topic pub /chatter std_msgs/String "data: Hello World"'],
        shell=True,
        env=proc_env,
        output='screen'
    )
    return LaunchDescription([publisher])

```

### Passing a yaml parameters file
```python
import os

from ament_index_python.packages import get_package_share_directory
from launch import LaunchDescription
import launch_ros.actions

def generate_launch_description():
    # Path the parameters file
    parameters_file = os.path.join(
        get_package_share_directory('some-package'),
        'config', 'parameters.yaml'
    )

    parameter_blackboard = launch_ros.actions.Node(
            package='demo_nodes_cpp', node_executable='parameter_blackboard',
            parameters=[parameters_file,]
            )

    return LaunchDescription([parameter_blackboard])
```
