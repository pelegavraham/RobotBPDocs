Rotate
===========


Event description
------------------

**Event name:** Rotate

**Params:** Json that specifie for each port on the boards the speed and angel the motor spin. 

**Description:** The program get the speed and angle for each port, check the motors which connect to them, 

and spin the robot's motors acoording to those speeds and angels. 


Json structure
----------------

First, select the key as the type of the board "EV3" or "GrovePi". 

The value of the type can be one from the two options:

If you have only one board of this type, the value can be array that contain the speed and the angel.

The second option, the value will be a json such that the key will be the index of the board, depending on how it is written in the build event,

and the value will be json when the key is the port that the motor connect to, and the value is the speed, for the board'th.

for example if you have one EV3 and motors that connected to port "B" and "C", the json will be in this structure:

.. code-block:: javascript
  :linenos:

    bp.sync({request: bp.Event("Rotate", {"EV3": {"B": [,], "C": [,]}})});

The value of keys "B" and "C" will be that speed and angel you want the motor move respectively.

The ports in the keys can be: 

For EV3 ports: "1", "2", "3", "4" "A" "B" "C" "D"

For Grove pi ports: "A0", "A1", "A2", "D0", "D1", "D2", "D3", "D4", "D5", "D6", "D7", "D8" 



Example
----------

.. code-block:: javascript
  :linenos:

    bp.registerBThread("Pickup in 90 degree", function(){
            bp.sync({request: bp.Event("Rotate", {"EV3": {"B": [10,90], "C": [10,90]}})});
        }
    });