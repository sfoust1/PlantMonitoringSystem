
# Plant Monitor System

 ## Goal of this project
  To demonstrate the ability to combine several services, several languages, into one maintainable and extensible project.

 ## What is this project
  This project is meant to provide analysts the ability to securely monitor, analyze, and manage metrics from a sensor monitoring system (SMS).
  This SMS will be geared towards the health and state of a plant system, including: air/soil humidity, temperature, and sun light. However, the goal is to provide an architecture to allow this list to grow with minimal maintenance. 
  This data will be access-controlled and viewable through a quick access web application or deep view through Tableau.
  The various technologies integrated are there with the goal of providing failover for the servers (backend/postgres), alert management, and ease/speed of deployment.

---
 ## Services To Be Integrated
  1. [Backend](#Backend)
   * [Containerization](#Docker)
   * [Processing Servers](#C++-Based-Servers)
   * [Sensor Monitoring System (SMS)](#Microcontroller)
   * [Application Management](#Application-Management)
   * [Alert Management - Messaging Queue (MQ)](#Zookeeper-Qpid)
   * [Database](#Postgres)
   * [Logging](#Logging)
  2. [Frontend](#Frontend)
   * [Web Application](#Node.js)
   * [Analytics](#Tableau)
   * [Alexa](#Alexa)
---
 ## <u>Backend</u>
 The backend will be responsible for connecting the frontend users to the database, load balancing connections amongst several servers, monitoring the health of the applications (SMS, servers, database),  sending any alerts heard from the SMS (to frontend users) or from the crashing of an application (to the admin), automatically launching backup containers (previously working versions of an application) should a new version crash, and monitoring sensors via SMS.
  ### Docker
   * Grow the backend horizontally, spinning up new servers as needed.
   * Have backup containers ready to launch in the event that a new version crashes and the old version needs to be spun up.
     * Should a container crash, also log the details in a log file and alert the admin 
   * Quickly provide an environment for which the applications are known to run in.

  ### C++ Based Servers
   * There will be one frontend server that will load balance the users connections to the processing servers.
   * Authentication: 
     * Front-end will be kerberos or ldap ( web application, Tableau ), and SSL cert ( Alexa, Application Management )
     * Back-end will be SSL certs
   * The processing servers will manage the users connection to the database (providing data and alerts from the SMS) and to modify the SMS parameters.
   * These will exist in the Docker Containers.
   * These servers will always produce logs for each users connections times and any updates to the SMS, as well as some application entry points.
   * These logs MAY produce detailed logs from applications, with the idea that a sigterm signal sent can up these levels mid-run to debug should a server seem stuck
   * When a process is started, an alert is sent to the database with a timestamp and other information. When finished, it remove that entry and place the action and details in a different table.

  ### Microcontroller
 This will be an ATmega328P based chip, the Arduino UNO+WiFi. 
   * A sensor monitoring system that will report data to the database
     * Ambient temperature
     * Ambient humidity
     * Soil humidity
     * Solar presence
   * This device will act wirelessly
   * Capabile of remote EEPROM
   * Will report if any thresholds are breached. Thresholds include:
     * Temperature HighCrit/LowCrit, HighWarn/LowWarn
     * Soil humidity HighCrit/LowCrit

  ###  Zookeeper Qpid
   * This will be how alerts are sent from the sensor systems and application monitor to the C++ Servers.
   * The Application Management Tool (docker crashes and log locations), Alexa (friendly SMS alert awareness), and Web Application (SMS alert notices) will all subscribe to these.

  ### Postgres
   * The database for storing sensor data, alerts, maybe server information, and also perhaps current sensor thresholds limits
---
 ## <u>Frontend</u>

  ### Node.js
   * Front-end will web application to monitor data points and remotely manage the SMS
     * This will be a web application that can:
     * View hourly/daily/weekly averages and current data collected from the Raspberry Pi sensors

  ### Tableau
   * This will be for analyzing data logged in the database.
 
  ### Alexa
   * For logging events outside of sensory data (when and how much water)
   * Alexa is chosen because the event is simple, and otherwise logging the event would be tedious.

  ### Application Management
   * Monitor the state of a docker container/application
   * Allow an admin to monitor who is attached to the servers
   * Should an action take too long to execute, automatically up the log levels and alert admin to investigate
   * Monitor and acknowledge alerts
     * Log notes about the alert
   * Remotely flash the Rasberry Pi with software updates
     * data-collection rates


 




