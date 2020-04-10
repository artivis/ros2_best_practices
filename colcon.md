# Colcon

Run a clean build:

    $ colcon build --cmake-clean-first --cmake-clean-cache

How to run the tests of a given package while actually seeing the test output:

    $ colcon test --packages-select <package name> --event-handlers console_direct+

How to run a specific test:

    $ colcon test --packages-select <package name> --pytest-args -k <test function name>

How to disable pytest captures (and output stdout/stderr) :

    $ colcon test --pytest-args -s

How to obtain test coverage of a given package:

    $ colcon test --packages-select <package name> --event-handlers console_direct+ --pytest-args --cov=<python package>
