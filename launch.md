# Launch

Find the doc [here](https://index.ros.org/doc/ros2/Tutorials/Launch-system/).

Find the [presentation at ROSCon 2018](https://roscon.ros.org/2018/presentations/ROSCon2018_launch.pdf).


### Passing launch prefix

```python
from launch import LaunchDescription
import launch.actions

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

### A `launch-prefix` wrapper
```python
#!/usr/bin/env python3

# Copyright 2019 Canonical, ltd.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Launch file that wraps another launch file to be called with a 'launch-prefix'.

usage:

$ ros2 launch <somewhere> launch_prefix.launch.py pkg:=<pkg-name> launch:=<launch-file> args:=<launch-prefix-args>

e.g.

$ ros2 launch <somewhere> launch_prefix.launch.py pkg:=demo_nodes_cpp launch:=talker_listener.launch.py args:=valgrind
"""

import os

from launch import LaunchDescription
from launch.launch_description_sources import PythonLaunchDescriptionSource
import launch.actions
import launch_ros.actions

def generate_launch_description():
    # Necessary to get real-time stdout from python processes:
    proc_env = os.environ.copy()
    proc_env['PYTHONUNBUFFERED'] = '1'

    ld = LaunchDescription([
      launch.actions.DeclareLaunchArgument('pkg'),
      launch.actions.DeclareLaunchArgument('launch'),
      launch.actions.DeclareLaunchArgument('args', default_value=''),
    ])

    ld.add_action(launch.actions.SetLaunchConfiguration('launch-prefix', launch.substitutions.LaunchConfiguration('args')))

    ld.add_action(launch.actions.IncludeLaunchDescription(PythonLaunchDescriptionSource([
                  launch_ros.substitutions.FindPackage(launch.substitutions.LaunchConfiguration('pkg')), '/share/',
                  launch.substitutions.LaunchConfiguration('pkg'), '/launch/',
                  launch.substitutions.LaunchConfiguration('launch')])))

    return ld
```
