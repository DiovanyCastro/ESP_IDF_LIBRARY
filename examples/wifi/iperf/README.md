| Supported Targets | ESP32 | ESP32-C2 | ESP32-C3 | ESP32-C6 | ESP32-S2 | ESP32-S3 |
| ----------------- | ----- | -------- | -------- | -------- | -------- | -------- |

# Iperf Example

## Note about iperf version
The iperf example doesn't support all features in standard iperf. It's compitable with iperf version 2.x.

## Note about 80MHz flash frequency
The iperf can get better throughput if the SPI flash frequency is set to 80MHz, but the system may crash in 80MHz mode for ESP-WROVER-KIT.
Removing R140~R145 from the board can fix this issue. Currently the default SPI frequency is set to 40MHz, if you want to change the SPI flash
frequency to 80MHz, please make sure R140~R145 are removed from ESP-WROVER-KIT or use ESP32 DevKitC.

## Introduction
This example implements the protocol used by the common performance measurement tool [iPerf](https://iperf.fr/).
Performance can be measured between two ESP32s running this example, or between a single ESP32 and a computer running the iPerf tool

Demo steps to test station TCP Tx performance:

1. Build the iperf example with sdkconfig.defaults, which contains performance test specific configurations

2. Run the demo as station mode and join the target AP
   sta ssid password

3. Run iperf as server on AP side
   iperf -s -i 3

4. Run iperf as client on ESP32 side
   iperf -c 192.168.10.42 -i 3 -t 60

The console output, which is printed by station TCP RX throughput test, looks like:

>esp32> sta aptest
>
>I (5325) iperf: sta connecting to 'aptest'
>
>esp32> I (6017) event: ip: 192.168.10.248, mask: 255.255.255.0, gw: 192.168.10.1
>
>esp32> iperf -s -i 3 -t 1000
>
>I (14958) iperf: mode=tcp-server sip=192.168.10.248:5001, dip=0.0.0.0:5001, interval=3, time=1000
>
>Interval Bandwidth
>
>esp32> accept: 192.168.10.42,62958
>
>0-   3 sec       8.43 Mbits/sec
>
>3-   6 sec       36.16 Mbits/sec
>
>6-   9 sec       36.22 Mbits/sec
>
>9-  12 sec       36.44 Mbits/sec
>
>12-  15 sec       36.25 Mbits/sec
>
>15-  18 sec       24.36 Mbits/sec
>
>18-  21 sec       27.79 Mbits/sec


Steps to test station/soft-AP TCP/UDP RX/TX throughput are similar as test steps in station TCP TX.

See the README.md file in the upper level 'examples' directory for more information about examples.
