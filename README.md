# ZKLibrary
ZKLibrary is PHP library for reading and writing data to attendance device using UDP protocol. This library is useful to comunicate between web server and attendance device directly without any addition program.
This library is implemented in the form of class. So that you can create an object and use it functions.

Web server must be connected to the attendance device via Local Area Network (LAN). The UDP port that is used in this communication is 4370. You can not change this port without changing firmware of the attendance device. So, you just use it.

The format of the data are: binary, string, and number. The length of the parameter and return value must be vary.

## Example
```php
<?php
include "zklibrary.php";
$zk = new ZKLibrary('192.168.1.102', 4370);
$zk->connect();
$zk->disableDevice();
$zk->testVoice();
$zk->enableDevice();
$zk->disconnect();
?>
```


---


## Data Structrure
```php
Class ZKLibrary{
String ip;
Unsigned Short port;
Unsigned Long socket;
Unigned Long session_id;
String received_data;
String user_data[][];
String attendance_data[][];
Unsigned Long timeout_sec;
Unsigned Long timeout_usec;
}
```
## Functions
```php
__construct([$ip[, $port]])
```
Object constructor.
### Parameters
$ip 

IP address of device.

$port 

UDP port of device.

```php
__destruct()
```
Object destructor.

```php
connect([$ip[, $port]])
```
Function to make a connection to the device. If IP address and port is not defined yet, this function must take it. Else, this function return FALSE and does not make any connection.
### Parameters
$ip

IP address of the device.

$port

UDP port of the device.

```php
disconnect()
```
Function to disconnect from the device. If ip address and port is not defined yet, this function must take it. Else, this function return FALSE and does not make any changes.
```php
setTimeout([$sec[, $usec]])
```
Set timeout for socket connection.
### Parameters
$sec

Timeout in second.

$usec

Timeout in micro second.
```php
reverseHex($input)
```
Reverse hexadecimal digits.
```php
encodeTime($time)
```
Encode time to binary data.
### Paramaters
$time

String time in format YYYY-MM-DD HH:II:SS
### Return Value
Encoded time in binary format.

```php
decodeTime($data)
```
Decode binary data to time.
### Parameters
$data

Binary data from device. 
### Return Value
Dedoded time in string format.

```php
checkSum($p)
```
This function calculates the chksum of the packet to be sent to the time clock.
### Parameters
$p

Packet to be checked.
```php
createHeader($command, $chksum, $session_id, $reply_id, $command_string)
```
Create data header to be sent to the device.
### Parameters
$command

Command to the device in integer.
### Return Value
Data header in binary format.

```php
$checksum
```
Checksum of packet.

$session_id

Session ID of the connection.

$command_string

Data to be sent to the device.
### Return Value
Sum of data to be checked.
```php
checkValid($reply)
```
Check wether reply is valid or not.
### Parameters
$reply

Reply data to be checked.
```php
execCommand($command, $command_string = '', $offset_data = 8)
```
Send command and data packet to the device and receive some data if any.
### Parameters
$command

Command to the device in integer.

$command_string

Data to be sent to the device.

$offset_data

Offset data to be returned. The default offset is 8.
```php
getSizeUser()
```
Get number of user.
### Return Value
Number of registered user in the devive.
```php
getSizeAttendance()
```
Get number of attendance log.
### Return Value
Number of attendance recorded in the device.
```php
restartDevice()
```
Restart the device.
```php
shutdownDevice()
```
Shutdown the device.
```php
sleepDevice()
```
Sleep the device.
```php
resumeDevice()
```
Resume the device.
```php
changeSpeed($speed = 0)
```
Change transfer speed of the device. 0 = slower. 1 = faster.
### Parameters
$speed

Transfer speed of packet when the device comunicate to other device, i.e server.

Note: some device may be not supported fast speed.
```php
writeLCD($rank, $text)
```
Write text on LCD. This order transmit character to demonstrate on LCD, the data part 1, 2 bytes of the packet transmit the rank value which start to demonstrate, the 3rd byte setting is 0 , follows close the filling character which want to be transmit. May work in CMD_CLEAR_LCD when use this function.
### Parameters
$rank

Line number.

$text

Text to be demonstrated to LCD of the device.
```php
clearLCD()
```
Clear text from LCD.
```php
testVoice()
```
Test voice of the device.
```php
getVersion()
```
Get device version.
### Return Value
Version of the device in string format.
```php
getOSVersion($net = true)
```
Get OS version.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setOSVersion($osVersion)
```
Set OS version
### Parameters
$osVersion

Version of operating version.
```php
getPlatform($net = true)
```
Get OS version.
### Parameters
$net
If net set to true, function will return netto data without parameter name.
```php
setPlatform($patform)
```
Set platform.
### Parameters
$platform

Platform name.
```php
getFirmwareVersion($net = true)
```
Get firmware version.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setFirmwareVersion ($firmwareVersion)
```
Set firmware version.
### Parameters
$firmwareVersion

The version of firmware.
```php
getWorkCode($net = true)
```
Get work code.
### Parameters
$net
If net set to true, function will return netto data without parameter name.
```php
setWorkCode($workCode)
```
Set work code.
### Parameters
$workCode

Work code.

```php
getSSR($net = true)
```
Get SSR
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setSSR($ssr)
```
Set SSR.
### Parameters
$ssr

SSR.
```php
getPinWidth($net = true)
```
Get pin width.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setPinWidth($pinWidth)
```
Set pin width.
### Parameters
$pinWidth

Pin width
```php
getFaceFunctionOn($net = true)
```
Check wether face detection function is available or not.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setFaceFunctionOn ($faceFunction)
```
Set wether face detection function is available or not.
### Parameters
$faceFunction

Face function. 1 = available; 2 = not available.
```php
getSerialNumber($net = true)
```
get serial number of the device.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setSerialNumber($serialNumber)
```
Set serial number of the device.
### Parameters
$serialNumber

Serial number of the device.
```php
getDeviceName($net = true)
```
Get device name.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setDeviceName($deviceName)
```
Set device name.
### Parameters
$deviceName

The device name.
```php
getTime()
```
Get time of device from real time clock (RTC). The time resolution is one minute.
### Return Value
getTime return time as string with format YYYY-MM-DD HH:II:SS.
```php
setTime($t)
```
Set time of the device.
### Parameters
Time to be set with format YYYY-MM-DD HH:II:SS.
```php
enableDevice()
```
Ensure the machine to be at in the normal work condition, generally when data communication shields the machine auxiliary equipment (keyboard, LCD, sensor), this order restores the auxiliary equipment to be at the normal work condition. 
```php
disableDevice()
```
Shield machine periphery keyboard, LCD, sensor, if perform successfully, there are showing “working” on LCD.
```php
enableClock()
```
Set the LCD dot (to glitter ‘:’) the packet data part transmit 0 to stop glittering, 1 start to glitter. After this order carries out successfully, the firmware will refresh LCD.
```php
getUser()
```
Retrive the user list from the device.
### Return Value
getUser return array 2 dimension. The key of array is serial number of user. The value of array is array containing: 
* serial number of the user
* user name
* user role
* user password
```php
setUser($uid, $userid, $name, $password, $role)
```
Write user to the device.
### Parameters
$uid

Serial number of the user. This is the unsigned short number (2 bytes).

$userid

User ID of the application. The maximum length of $userid is 8 characters containing numeric whithout zero on the beginning.

$name

User name. The maximum length of $name is 28 characters containing alpha numeic and some (not all) punctuation.

$role

The role of user. The length of $role is 1 byte. Possible value of $role are:
```
0 = LEVEL_USER
2 = LEVEL_ENROLLER
12 = LEVEL_MANAGER
14 = LEVEL_SUPERMANAGER
```
```php
clearData()
```
Clear some kind of data, if do not assign the data type, then deletes all data, otherwise depending on the assigned type to delete data.
```php
clearUser()
```
Same with clearData.
```php
deleteUser($uid)
```
Delete some user from the device.
### Parameters
$uid

Serial number of the user (2 bytes).
```php
deleteUserTemp($uid, $finger)
```
Delete finger template of the user from the device.
###
Parameters
$uid

Serial number of the user (2 bytes).

$finger

The number of finger (0-9).
```php
clearAdmin()
```
Delete all admin from the device.
```php
getAttendance()
```
Retrieve the attendance log.
### Return Value
getAttendance return array 2 dimension. The value of array is array containing.
* serial number of the user
* user id of the application
* state
* time of attendance in format YYYY-MM-DD HH:II:SS
```php
clearAttendance()
```
Delete all attendance log from the device.
