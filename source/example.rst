.. _exampels:

Project example
================

.. code-block:: java
  :linenos:

  var allEventsButBuildEventSet = bp.EventSet("Block all for build", function (e) {
      return !e.name.equals("Build");
  });

  var dataEventSet = bp.EventSet("", function (e) {
      return e.name.equals("GetSensorsData");
  });

  var AlgorithmEventSet = bp.EventSet("", function (e) {
      return e.name.equals("GetAlgorithmResult");
  });

  var direction = 1;

  bp.registerBThread("Do Something with Data", function () {
      bp.sync({request: bp.Event("Subscribe", {"GrovePi": ["D4"]})});

      while (true) {
          var e = bp.sync({waitFor: dataEventSet});
          var data = JSON.parse(e.data);
          var distance  = data.GrovePi._1.D4;
          if (distance < 15){
              direction = -1 * direction ;
          }
      }
  });

  bp.registerBThread("Just Right", function () {
      bp.sync({request: bp.Event("Subscribe", {"EV3": ["2"]})});

      while (true) {
          var e = bp.sync({waitFor: dataEventSet});
          var data = JSON.parse(e.data);
          var distance  = data.EV3._1._2;
          if (distance > 15 && distance < 20){
              bp.sync({request: bp.Event("Rotate", {"EV3": {"B": 60, "C": 60, "speed": 15}})});
          }
      }
  });

  bp.registerBThread("Too Far Right", function () {
      bp.sync({request: bp.Event("Subscribe", {"EV3": ["2"]})});

      while (true) {
          var e = bp.sync({waitFor: dataEventSet});
          var data = JSON.parse(e.data);
          var distance  = data.EV3._1._2;
          if (distance > 20){
              bp.sync({request: bp.Event("Rotate", {"EV3": {"B": 30, "C": 60, "speed": 15}})});
          }
      }
  });

  bp.registerBThread("Too Far Left", function () {
      bp.sync({request: bp.Event("Subscribe", {"EV3": ["2"]})});

      while (true) {
          var e = bp.sync({waitFor: dataEventSet});
          var data = JSON.parse(e.data);
          var distance  = data.EV3._1._2;
          if (distance < 15){
              bp.sync({request: bp.Event("Rotate", {"EV3": {"B": 60, "C": 30, "speed": 15}})});
          }
      }
  });

  bp.registerBThread("Do My Algorithm", function () {
      bp.sync({request: bp.Event("MyAlgorithm", {"EV3": {1: {"Param1": 10, "Param2": {"Param2_1" : "Hello"}}}, "GrovePi": {2: {"Param3": 100}}})});
      var e = bp.sync({waitFor: AlgorithmEventSet});
      var data = JSON.parse(e.data);
      bp.sync({request: bp.Event("Test", data)});
  });


  bp.registerBThread("Initiation", function () {
      bp.sync({
          block: allEventsButBuildEventSet, request: bp.Event("Build",
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
          )
      })
  });