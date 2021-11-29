# Tasks
This document was basically a helper to creating the task placement document

## Message Queue (MQ)
-	Download and install Zookeeper/Qpid.
-	Determine required qpid configurations
-	Start both Zookeeper and Qpid
-	Determine messaging schema
-	Determine what applications need to send what messages

## Postgres Database
-	Download postgres version 13.
-	Determine best method for standing up postgres server in a quick/repeatable manner
-	Determine access methods for each application/admin
-	Determine schema needed for all applications

## Sensor Monitoring System
-	Purchase device
-	Purchase ambient humidity sensor
-	Purchase soil humidity sensor
-	Purchase solar sensor
-	Write function for connecting to database
-	Write function for writing to the database
-	Write function for sending alerts to MQ
-	Write function to regularly report running state to MQ
-	Write function for accessing sensors
  - Determine hi/hiWarn/loWarn/lo
  - Determine and write code for how often records should be reported to database
-	Write function for accessing soil humidity
  - Determine hi/hiWarn/loWarn/lo for humidity
  - Determine and write code for how often records should be reported to database
-	Write method for flashing EEPROM with HI/Lo Alerts

## Process Server
-	Write function for accepting incoming connections, reporting connection to MQ
  - May need to interface with Dev Sec Ops to determine what IP address server will listen on
-	Write function for connection to database
-	Write master catch that will propagate all subclass catches to MQ
-	Write function that will report start and stop times to MQ
-	Write SQL Queries that will provide latest sensor levels
-	Write function that will force client to get updated reports in case of threshold exceedance
-	Write function that will allow a user to resolve an alert with a short description of the event, sending that data into the database.
-	Write functions that will report start and stop time of functions
  - The reporting of these alerts will be controlled by debug levels
  - Master will always report, individual sub level functions will be variable depending on software architects determinations
-	Function that will listen for a request to close connection

## Load Balancer
-	Write function for determining how many users are connected to a server
-	Write function for determining what servers are up and running
-	Write function for determining CPU usage in a servers container
-	Write function that will spin up a new process server container and register the ip address with the postgres database
  - This will also send alert to MQ about new connection
-	Write function for returning which IP address a client should connect to.
-	Write function for authenticating a users’ connection

App Management
-	Write listener for alerts
  - SMS exceedance
  - Client Command process server execution exceedance
  - Process server crash report
-	Write GUI that will have:
  - status on each clients connections
  - time connected
  - current command
    - command time start
    - execution time status alert
-	Write function that will periodically status the postgres server and display status in GUI
-	Write function that will execute an EEPROM flash to SMS

## Web Application
-	Connection to Load Balancer
-	Ability to take IP address returned from Load Balancer and then connect there instead
-	GUI displays sensor data
-	Login
-	Text field allowing resolution of sensor
-	Ability to send request to disconnect from server

## Alexa
-	Connect directly to postgres database
-	Write function that will listen to botanists recordings on water log
  - How much water in liters is being administered
  - Visual determinations on plant status
    - Determine simple status reports
  - Visual description of plant status

## Tableau
-	Connection to postgres database directly
