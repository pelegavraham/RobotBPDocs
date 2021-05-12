Set sensor
============


Event description
------------------

**Event name:** SetSensor

**Params:** Json that specifie the ports on the boards that you want to set the data of the sensors that connected them.

**Description:** The program get the ports and the data, check the sensors which connect to them, 

and set the values of the sensors to the data.


Json structure
----------------

First, select the key as the type of the board "EV3" or "GrovePi". 

The value of the type can be one from the two options:

If you have only one board of this type, the value is double to set, in the case of boolean 1.0 is true and 0.0 is false

The second option, the value will be a json such that the key will be the index of the board, depending on how it is written in the build event,

and the value is json which the key is the port string and the value is double to set, in the case of boolean 1.0 is true and 0.0 is false.

for example if you have one Grove pi the json will be in this structure:

.. code-block:: javascript
  :linenos:

    bp.sync({request: bp.Event("SetSensor", {"GrovePi": {}})});

in the json the key port you can select from the strings below: 

For EV3 ports: "1", "2", "3", "4" "A" "B" "C" "D"

For Grove pi ports: "A0", "A1", "A2", "D0", "D1", "D2", "D3", "D4", "D5", "D6", "D7", "D8" 

and the value is double, as mention.

Example
----------

.. code-block:: javascript
  :linenos:

    bp.registerBThread("Change data", function () {
        bp.sync({request: bp.Event("SetSensor", {"GrovePi": {"A0":1.0}})});
    });
   