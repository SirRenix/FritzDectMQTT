# Changelog


## Version 1.1.01 - 2024-10-24
### Fixes
- **MQTT Reconnection Fix**: Added a reconnection check for fritzconnection to handle scenarios where the MQTT client is disconnected. The script now waits for 5 seconds before retrying the connection if the client is not connected, ensuring continuous attempts until a successful reconnection is made.
Downtime check ~20min.

## Version 1.1 - 2024-10-23
### Fixes
- **Improved**: Improved automatic reconnection to the MQTT broker after a connection loss. Exception handling has also been implemented. This fix fixes problems where the script no longer restores a connection. Seconds of network downtime did not affect the script.

### Changes
- **Logging Improvements**: Improved logging during reconnection attempts and after successful reconnections.
- **Code Optimization**: Minor refactoring for better readability and maintainability.

## Version 1.0 - Initial Release
- Initial release of FritzDectMQTT with basic functionality for reading DECT socket data from Fritzbox and sending it to an MQTT broker.
- Includes support for threading, basic home automation commands, and MQTT message sending and receiving.
