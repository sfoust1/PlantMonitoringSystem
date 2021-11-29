## Dev Sec Ops
-	Ensure developers have the tools they need to accomplish their tasks

### Message Queue (MQ) Standup
- Define connection characteristics

### Postgres Standup
- Define connection characteristics
- Write postgres schema load scripts
- Write postgres dump/cleanup methodologies
  - Dump is for backups
  - Cleanup is for keeping database size minimal while keeping historical data
-	Ensure developers have the tools they need to accomplish their tasks

### Docker
-	Develop docker methodologies to encapsulate:
  - Postgres
  - Load Balancer
  - Process Server

### Authentication Tool
-	Stand up authentication tool
-	Set up Tableau
-	SMS EEPROM Flashing


## Backend Developers
### Process Server
- Client connection management
  - Connection
  - Authentication
  - Usage log
- MQ connection
- Application crash management
  - Try/catch
  - MQ report log file location to application management
  - Text file logging report
- Function execution times
- DAR
- Passing threshold exceedance to client
- SIGINT Management
  - Increased log levels

### Web Application
- Server connection management
  - Connection
  - Authentication
- DAR
- Data Reporting Rate

### Application Management
- MQ Connection
- Postgres statusing
- Task exceedance management
- EEPROM Flash target/all SMS

### Sensor Monitoring System
- DAR
- Sensor Access Routines
- Threshold management

### Postgres
- “Hello, World” example
  - C++
  - C
  - Alexa
  - Node.js
- Develop connection classes
  - C++
  - C
  - Alexa
- IP/Host name resolution
- Develop data access routines
 
 ### MQ
- “Hello, World” example
  - C++
  - C

### Alexa
- DAR

## Front-end developers
### Web Application
- Login page
- Main landing
  - Alert frame
    - Plant ID
    - Alert type
    - Alert Reading
    - Alert measuring unit
    - Alert time
    - Text Field – Resolution Description
    - Submit Resolution
  - Side bar for available plants to observe
    - Averages
      - Day
      - Week
  - Various sensor data, current/expected, with status light
    - Green – Good
    - Yellow – Warn
    - Red – Critical

### Application Management
- Main landing
  - List of connections
    - Client user
    - Client connection time
    - Last client command
    - Drop down of all commands should log levels be up
    - Line number within code
    - Command status
      - Green – On Track
      - Red – Exceeded limit
- SMS Management
  - Drop down of plants available to manage or all
  - EEPROM Flash button

### Alexa
- Voice input routing
- Alert reporting
