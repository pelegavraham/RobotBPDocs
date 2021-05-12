Subscribe
=============


Event description
------------------

**Event name:** Subscribe

**Params:** Json that specifie the ports on the boards that you want to track after the data that belong them.

**Description:** The program get the ports, check the sensors which connect to them, 

and keep track after the values that back from the robot's sensors every time cycle


Json structure
----------------

First, select the key as the type of the board "EV3" or "GrovePi". 

The value of the type can be one from the two options:

If you have only one board of this type, the value can be array of strings which presnet the ports name.

The second option, the value will be a json such that the key will be the index of the board, depending on how it is written in the build event,

and the value will be array of strings which presnet the ports name the connected to the board'th.

for example if you have two EV3 and one Grove pi the json will be in this structure:

.. code-block:: javascript
  :linenos:

    bp.sync({request: bp.Event("Subscribe", {"EV3": {1: [], 2: []}, "GrovePi": []})});

in array you can select from the strings below: 

For EV3 ports: "1", "2", "3", "4" "A" "B" "C" "D"

For Grove pi ports: "A0", "A1", "A2", "D0", "D1", "D2", "D3", "D4", "D5", "D6", "D7", "D8" 



Example
----------

.. code-block:: javascript
  :linenos:

    var dataEventSet = bp.EventSet("", function (e) {
        return e.name.equals("GetSensorsData");
    });

    bp.registerBThread("Do Something with Data", function () {
        bp.sync({request: bp.Event("Subscribe", {"EV3": {1: ["2"], 2: ["3"]}, "GrovePi": ["D3"]})});
        bp.sync({request: bp.Event("Update")});
        var e = bp.sync({waitFor: dataEventSet});
        var data = JSON.parse(e.data);
        var s  = data.EV3._1._2;
        // do something with s
    });
   