.. _setup:

Setup instructions
===================================

1. setting up the raspberry pi
--------------------------------

Your first steps with the raspberry pi can be supported with this `site <https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started>`_.

After you finish to configure the raspberry pi, you can connect him from your local computer via VNC viewer. 

To download VNC click `here <https://www.realvnc.com/en/connect/download/viewer/>`__.

The connection between the comuter and the raspberry made in the VNC by entering the ip of the raspberry with the user name and password you defined at the installation.

2. setting up the grove pi
----------------------------

The connection between the raspberry and the grove is made physically by adding the grove above the raspberry. 

As you can see in the picture:

.. figure:: /images/merge_ras_and_grov.jpg

3. setting up the EV3
-----------------------

The connection between the raspberry and the EV3 is made via bluetooth. 

To configure the bluetooth connection follow the instroductions `here <https://www.lego.com/en-us/service/help/products/themes-sets/mindstorms/connecting-with-bluetooth-to-lego-mindstorms-ev3-apps-408100000007982>`__.

4. prepare your coding environment
-------------------------------------

For your convenience, your coding can be done in your local computer and the running will apply directly on the raspberry pi. 

If you use intellij, first you need to add the extension: "Embedded Linux JVM". 

Go to ``Edit Configuration`` and add new configuration ``Embedded Linux JVM``. 

Then enter the ``Hostname`` (ip), ``Username`` and ``Password`` of the raspberry, and define the ``Moudle`` and ``Main Class``.

If you use eclipse move to intellij :) 

5. install RabbitMQ
---------------------

In the code that provide to you, there is communication between the commands that send to the robot from the user and the data that back from the robot.

The communication implemented in platform who called: RabbitMQ.

To download RabbitMQ on the raspberry-pi follow the instroductions `here <https://www.rabbitmq.com/install-debian.html>`__.

6. Download the code from github
----------------------------------

link to Robot repo: https://github.com/Dave-Zi/Robot

link to RobotActorator repo: https://github.com/Dave-Zi/RobotActuator

link to BPjsRobotProject repo: https://github.com/Dave-Zi/BPjsRobotProject

link to RobotUtils repo: https://github.com/Dave-Zi/RobotUtils


.. admonition:: Note!

   As mention before, the Raspberry Pi is MUST to be installed as part of the robot. 

   The EV3 and Grove Pi are additional recommended parts, to get more exciting actions from your robot.  
