# Colcon

How to run the tests of a given package while actually seeing the test output:

    $ colcon test --packages-select <package name> --event-handlers console_direct+

How to obtain test coverage of a given package:

    $ colcon test --packages-select <package name> --event-handlers console_direct+ --pytest-args --cov=<python package>
