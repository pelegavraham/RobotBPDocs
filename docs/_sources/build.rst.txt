Build
=======

Event description
------------------

**Event name:** Build

**Params:** Json that describe the boards and their details. 

If the board is instance of EV3, for the key "Port" 

we specifie the name of the port the bluetooth connect to the raspberry pi.

If the board is instance of Grove pi, for the key of each port 

we specifie the name of the sensor that connect to the port.

**Description:** The program get the boards and ports which connected to them 
and build their instances in the system and connect them.


Json structure
----------------

The parameter of the json must be with specifice structure

You can select what kind of boards you use, in each board the dictionary is detemenistic with the same keys. 

for example if you select one EV3 and one Grove pi the json will be in this structure:

.. code-block:: javascript
  :linenos:

    {
        "EV3":
            [{
                "Port": ""
            }]
        ,
        "GrovePi":
            [{
                "A0": "",
                "A1": "",
                "A2": "",
                "D2": "",
                "D3": "",
                "D4": "",
                "D5": "",
                "D6": "",
                "D7": "",
                "D8": ""
            }]
    }

in the values you put : 

For EV3 port: the name of the port the bluetooth connect to the raspberry pi.

For Grove pi ports: The optional sensors that the system support with, are:

* "Led"

* "Ultrasonic"

* "Sound"

* "Button"

* "Rotary"

* "Relay"

* "Light"

* "Buzzer"

* "Temperature DHT11"

* "Temperature DHT21"

* "Temperature DHT22"

* "Temperature AM2301"

The ports of the gorve pi are A0-A2 and D0-D8

Example
----------

.. code-block:: javascript
  :linenos:

   var allEventsButBuildEventSet = bp.EventSet("Block all for build", function (e) {
       return !e.name.equals("Build");
   });


   bp.registerBThread("Initiation", function () {
       bp.sync({block: allEventsButBuildEventSet, request: bp.Event("Build",
               {
                   "EV3":
                       [{
                           "Port": "rfcomm0"
                       }]
                   ,
                   "GrovePi":
                       [{
                           "A0": "",
                           "A1": "",
                           "A2": "",
                           "D2": "Led",
                           "D3": "",
                           "D4": "Ultrasonic",
                           "D5": "",
                           "D6": "",
                           "D7": "",
                           "D8": "Led"
                       }]
               }
               )})
   });


.. warning::
   
   The "Build" Event must to execute first, because all the other events 

   depends on the robot that must build in our program first.