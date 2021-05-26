Appendices
===========

- 	The robot is slower than BPjs, and it may be overflowed with commands and this can cause lost of commands.
	make sure you don't send to many commands together (especially not in while(true)).

- 	When adding a new functionality to CommandHandler in RobotActuator - you might want to test it,
	use the TestBoard object for these tests if needed.
	This will allow you to test methods without connecting the robot.

- 	When updating one of the projects - make sure you run 'mvn deploy' command to update the maven dependency.

- 	Make sure 'build' is always the first event to run.

-	When running 'RobotActuator' project, make sure it run on the RaspberryPi.