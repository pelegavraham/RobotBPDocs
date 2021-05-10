Drive 
===========

Event description
------------------

**Event name:** Drive 

**Params:** Json that specifie for each port on the boards the speed the motor move on. 

**Description:** The program get the ports and the speeds, check the motors which connect to them, 

and acturate the robot's motors acoording to those speeds. 


Json structure
----------------

First, select the key as the type of the board "EV3" or "GrovePi". 

The value of the type can be one from the two options:

If you have only one board of this type, the value can be json when the key is the port that the motor connect to, and the value is the speed.

The second option, the value will be a json such that the key will be the index of the board, depending on how it is written in the build event,

and the value will be json when the key is the port that the motor connect to, and the value is the speed, for the board'th.

for example if you have one EV3 and motors that connected to port "B" and "C", the json will be in this structure:

.. code-block:: javascript
  :linenos:

    bp.sync({request: bp.Event("Drive", {"EV3": {"B": , "C": }})});

The value of keys "B" and "C" will be that speed you want the motor move.

The ports in the keys can be: 

For EV3 ports: "1", "2", "3", "4" "A" "B" "C" "D"

For Grove pi ports: "A0", "A1", "A2", "D0", "D1", "D2", "D3", "D4", "D5", "D6", "D7", "D8" 



Example
----------

.. code-block:: javascript
  :linenos:

    bp.registerBThread("Align to Left Wall", function(){
        bp.sync({request: bp.Event("Subscribe", {"EV3": ["2"]})});

        var speedOffset = 0;
        while (true) {
            var e = bp.sync({waitFor: dataEventSet});
            var data = JSON.parse(e.data);
            var myDistance = data.EV3._1._2; // get data from port 2 on Ev3

            if (myDistance == null){
                continue;
            } else if (myDistance > 10) { // Offset is incrementally changed to slowly fix direction until wall is found and aligned with.
                speedOffset = Math.max(speedOffset, 0); // speedOffset is reset to 0 if it was negative
                speedOffset = Math.min(20, speedOffset + 5); // Incrementally add 1 to the speed offset to max difference of 10
            } else if (myDistance < 10) {
                speedOffset = Math.min(speedOffset, 0); // speedOffset is reset to 0 if it was positive
                speedOffset = Math.max(-20, speedOffset - 5); // Incrementally subtract 1 to the speed offset to max difference of 10
            } else {
                speedOffset = 0
            }
            bp.sync({request: bp.Event("Drive", {"EV3": {"B": 20 - speedOffset, "C": 20 + speedOffset}})});
        }
    });