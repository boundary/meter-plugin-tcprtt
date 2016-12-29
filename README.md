TrueSight AppRTT Plugin
---------------------------

Displays App Round Trip Time for specific flows subscribed to meter.

### Prerequisites

|     OS    | Linux | Windows | SmartOS | OS X |
|:----------|:-----:|:-------:|:-------:|:----:|
| Supported |   v   |    v    |    v    |  v   |


### Plugin Setup

#### Enabling TCP Timestamp option
In order to provide the application round trip time metric, the optional TCP timestamp settings must be enabled on the target OS.  Depending on the OS, it may or may not be enabled by default.
The table below shows the currently supported OS's and how to enable the flag.

|     OS              |   Enable Command                              | Default setting |
|:--------------------|:---------------------------------------------:|:---------------:|
| OS/X 10.8 to 10.10	|  sudo sysctl net.inet.tcp.rfc1323=1           |  Enabled        |
| OS/X 10.11         	|  Unknown - feature was removed                |  Unknown        |
| Windows 2008/2012 	|  netsh int tcp set global timestamps=enabled  |  Enabled        |
| Ubuntu            	|  echo 1 > /proc/sys/net/ipv4/tcp_timestamps   |  Enabled        |
| CentOS            	|  echo 1 > /proc/sys/net/ipv4/tcp_timestamps   |  Enabled        |
| FreeBSD            	|  sudo sysctl net.inet.tcp.rfc1323=1           |  Enabled        |
| Ubuntu            	|  echo 1 > /proc/sys/net/ipv4/tcp_timestamps   |  Enabled        |
| ArchLinux         	|  echo 1 > /proc/sys/net/ipv4/tcp_timestamps   |  Enabled        |
| OpenSuse          	|  echo 1 > /proc/sys/net/ipv4/tcp_timestamps   |  Enabled        |
| Alpine            	|  echo 1 > /proc/sys/net/ipv4/tcp_timestamps   |  Enabled        |

#### Filter JSON value syntax/semantics
For subscriptions to flows, the filter expression is an object like the following:
{
 "options": {
  "include_loopback": true|false,
  "include_geoip":true|false
 },
 "topk": {
  "sorting_metric": "bits|packets|retransmits|out_of_order|handshake_rtt|app_rtt|disabled",
  "num_flows": <number between 1 and 25, inclusive>
 },
 "filters": [
 <an array of strings in BBPF (not PCRE) format, which are logically OR'd together by the flow filter logic>
 ]
}
 
 
#### Plugin Configuration Fields
|Field Name        |Description                                                                                                                                                                                                                                                    |
|:-----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|filter            |The JSON filter value to subscribe meter channel.                                                                                                                                                                                                          |
|Polling Interval|A numeric value representing polling interval time in miliseconds (ex 1000 for 1 Sec).                                                                                                                                                                                                    |

### Metrics Collected

|Metric Name   |Description                                                             |
|:-------------|:-----------------------------------------------------------------------|
|APP RTT       |Application round trip time                                             |

