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
    publisher = ExecuteProcess(
        cmd=['ros2 topic pub /chatter std_msgs/String "data: Hello World"'],
        shell=True,
        output='screen'
    )
    return LaunchDescription([publisher])

```
