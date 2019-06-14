# Launch

Find the doc [here](https://index.ros.org/doc/ros2/Tutorials/Launch-system/).

Find the [presentation at ROSCon 2018](https://roscon.ros.org/2018/presentations/ROSCon2018_launch.pdf).

### Passing launch prefix

```python
def generate_launch_description():

    ld = LaunchDescription(...)

    ld.add_action(launch.actions.SetLaunchConfiguration('launch-prefix', 'valgrind'))
```
