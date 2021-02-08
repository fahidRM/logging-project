# logging-project

This is a collection of sample jason projects that are capable of logging to the designed tool.


#### How to use the logger with your Project (JASON only)

1. Include the `stag-lib.jar` library in your project as a dependency. [Download stag-lib.jar here](https://github.com/fahidRM/logging-project/releases/tag/1.0.0-beta).
2. To log an agent, set it to use the `jason_logger.LoggerAgArch` AgArch. 
   This can be done through the `mas2j` file as shown below;
   
   `agents: agent agentArchClass  jason_logger.LoggerAgArch;` 
   
   where `agent` is the agent's name.
   
3. Enable logging from the `asl` file by updating the initial goal as shown below;
   If your agent was:
   
   ` ! start.
     +! start <- true : .print('hello'); 
   `
   
   alter it to :
   
   
    `! init_logger_and_perform_initial_goal.
    +! init_logger_and_perform_initial_goal : true <- jason_logger.initialise; !start.
   `
                                                     
   
  


#### Logging Summary
For the benefit of future expansion and reference, the logging system expects 4 categories of logs. Namely;
`ACTION`, `PLAN_SELECTION`, `PLAN_TRACE` and `SENSE`.

- `ACTION` denotes actions taken by an Agent.
- `PLAN_SELECTION` denotes a selected plan path.
- `PLAN_TRACE` denotes all options availbale to an agent at a point.
- `SENSE` denotes sensor readings or belief-base

Kindly find the definition of each log type below:
`

      {
        "AGENT": "Alice", 
        "TYPE": "ACTION",
        "TYPE_INFO": {
          "IDENTIFIER": "move(1,0)",
          "CODE_LINE": 27,
          "CODE_FILE": "alice.asl"
        },
        "TIME_IN_MS": 1610281344629,
       "SECONDARY_TIMER": 5,
        "SEQUENCE_NUMBER": 5
      }
      
      {
         "MAS": "demo_mas",
         "AGENT": "Alice",
         "TYPE": "SENSE",
         "TYPE_INFO": {
              "ACTION": "DUMP",
              "VALUES": "action_completed(move)|percept;has_cattle|belief"
        },
          "TIME_IN_MS": 1610281344629,
          "SECONDARY_TIMER": 5,
          "SEQUENCE_NUMBER": 5
      }
      
      {
        "AGENT": "Alice",
        "TYPE": "PLAN_TRACE",
          "TYPE_INFO": [
              {
                "IDENTIFIER": "option_a",
                  "CONTEXT": "has_cat & has_bicycle",
                  "CODE_LINE": 17,
                  "CODE_FILE": "alice.asl"
              },
              {
                "IDENTIFIER": "option_a",
                  "CONTEXT": "has_cat & has_car"
                  "CODE_LINE": 32,
                  "CODE_FILE": "alice.asl"
              }
          ]
      }
      
      {
        "TYPE": "PLAN_SELECTION",
        "AGENT": "Alice",
        "TYPE_INFO": {
            "IDENTIFIER": "option_a",
            "CONTEXT": "has_cat & not has_bicycle",
            "CODE_LINE": 17,
            "CODE_FILE": "alice.asl"
        }
}
  `
