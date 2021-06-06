.. _setup:

Setup instructions
===================

1. Setting up the raspberry pi
--------------------------------

Your first steps with the raspberry pi, including familiarity with hardware and installation, can be supported
in this `site <https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started>`_.

After you finish to configure the raspberry pi, you can connect him from your local computer via VNC viewer. 
To download VNC click `here <https://www.realvnc.com/en/connect/download/viewer/>`__.

The connection between your local computer and the raspberry pi made in the VNC by entering the ip of the raspberry
with the user name and password you defined at the installation.

2. Setting up the grove pi
----------------------------

The connection between the raspberry and the grove is made physically by adding the grove above the raspberry. 

As you can see in the picture:

.. figure:: /images/merge_ras_and_grov.jpg
    :scale: 60 %

3. Setting up the EV3
-----------------------

The connection between the raspberry and the EV3 is made via bluetooth. 

To configure the bluetooth connection follow the introductions `here <https://www.lego.com/en-us/service/help/products/themes-sets/mindstorms/connecting-with-bluetooth-to-lego-mindstorms-ev3-apps-408100000007982>`__.

4. Prepare your coding environment
-------------------------------------

For your convenience, you can coding in your local computer and the running will apply directly on the raspberry pi.

If you use intellij, first you need to add the extension: ``Embedded Linux JVM``.

In the RobotActuator repository, Go to ``Edit Configuration`` and add new ``Embedded Linux JVM`` configuration.

Then enter the ``Hostname`` (ip), ``Username`` and ``Password`` of the raspberry pi,
and define the ``Module`` and the ``Main Class``.

5. Install RabbitMQ
---------------------

In the project, there is communication between the commands that send to the robot from the user and the data that back from the robot.

The communication implemented in platform who called: RabbitMQ. Is famous IOT communication protocol.

To download RabbitMQ on the raspberry pi follow the introductions `here <https://www.rabbitmq.com/install-debian.html>`__.

6. Download the code from github
----------------------------------

link to Robot repo: https://github.com/Dave-Zi/Robot

link to RobotActuator repo: https://github.com/Dave-Zi/RobotActuator

link to BPjsRobotProject repo: https://github.com/Dave-Zi/BPjsRobotProject

link to RobotUtils repo: https://github.com/Dave-Zi/RobotUtils

link to RobotBPDocs repo: https://github.com/pelegavraham/RobotBPDocs

Make sure there is no compilation errors, the project opens as Maven project and the jdk version at least 11.0.9.

.. admonition:: Note

   You don't need to download all the repos. For your first steps in the project you can download
   BPjsRobotProject and RobotActuator repos.
   If you later want to expand the project, you will need to download the other repos.