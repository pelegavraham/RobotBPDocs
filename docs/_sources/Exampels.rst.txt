.. _exampels:

Project exampels
====================

.. code-block:: java
  :linenos:

	RobotSensorsData robotSensorsData = new RobotSensorsData();
        commandHandler = new CommandHandler(robotSensorsData);
        CommunicationHandler communicationHandler = new CommunicationHandler("Data", "Commands");
        communicationHandler.setMyCallback(MainTest::onReceiveCallback);

        communicationHandler.openSendQueue(true);
        communicationHandler.openReceiveQueue(false);

        while (true){

            if (robotSensorsData.isUpdated()) {
                String json = robotSensorsData.toJson();
                communicationHandler.send(json);
            }
        }