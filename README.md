# NETWORK MONITORING

## Zabbix

Zabbix is an open-source network monitoring tool that monitors:
 - Networks, Servers, Apllications, Logs, Security Events, Cloud Infrastructure

 The tool monitors network devices via SNMP:

 - Interface Traffic, Errors, CPU load, Link Status, Device Uptime, Bandwidth Usage

In servers and host OSes via agent; it monitors

- CPU, RAM, Disk, Event Logs, Services, Processes, Logs

Zabbix can also trigger alerts when:

- Packet drops increase, Interface floods occur, CPU spikes

### Core Problems Solved by Zabbix

1. "We don't know when system fails"

    - continously checks device status
    - detects outages automatically
    - alerts immediately

2. "We don't know why performance is slow"

    - collects performance metrics
    - show trends
    - identifies bottlenecks

3. "We don't have visibility acroess infrastructure"

    Provides centralised monitoring for; routers, switches, servers, applications, services, logs.

4. "We can't detect abnormal behaviour early"

    - establishes normal baselines
    - detects deviations
    - triggers alerts

5. "Troubleshooting takes too long"

    Provides historical metrics:
    - bandwidth graphs
    - CPU graphs
    - Service uptime logs

6. "We can't measure reliability or SLA"

    Zabbix calculates; uptime percentage, availability reports, SLA Compliance used for audits and management reports



### SNMP

Simple Network Management Protocol is an application layer protocol used for monitoring, managing and queriyiing network devices such as routers, switches, servers, firewalls, printers and IoT endpoints.

It enables a centralised system to: 
- collect operational metrics
- detect faults 
- trigger alerts
- modify device parameters remotely

SNMP Communications types

GET - SET - TRAP

Example

    - Zabbix sends GET request to routers
    - Router checks MIB and replies with OID value of interface status
    - Router sends TRAP -> "Interface Down"

So I'm going to implement Zabbix in my Home Lab

![Home_Lab.png](./images/Home_Lab.png)

Reference: `https://www.zabbix.com/documentation/7.4/en/manual/installation/install_from_packages`

 ### Zabbix Installation

 Zabbix is going to be run in UbuntuServer-1 as a server. Actually it is going to be implemented for TheCoinSociety infrastructure (an imaginary company). For it to be easy; referencing to the website and implementing configuration; i'm going to access the server from UbuntuDesktop-1 remotely via SSH.

 So according to the official website I have to define the OS which is going to host zabbix server so that I can get corresponding installation procedures.

 ![Zabbix_Site.png](./images/)

 Then, I follow the process accordingly.

![Zabbix_1.png](./images/zabbix_1.png)

![Zabbix_2.png](./images/zabbix_2.png)

![Zabbix_3.png](./images/zabbix_3.png)

Zabbix Server has successfully been installed and is running as a service in Ubuntu Server. It is accessible via the server's IP `172.16.1.11/zabbix`(statically assigned IP).

In the UbuntuServer Zabbix is running as both a server and an agent.

This the the Zabbix Dashboard.

![Zabbix_4.png](./images/zabbix_4.png)

I am going to configure network devices with SNMPv2 so that is advertises information to the Zabbix Server and also add agents on Windows and Ubuntu Desktop.

![Zabbix_5.png](./images/zabbix_5.png)
Now devices are added to the Zabbix for monitoring. Device name `Inno` is an Ubuntu Desktop, turn it off to save my RAM usage.

Let me test one network device. I am going to turn off `interface serial 3/0` on TCS-Router. 

![Zabbix_6.png](./images/zabbix_6.png)

As you can see below; it work and also give information on the down time of the interface.

![Zabbix_7.png](./images/zabbix_7.png)

When I turned the interface up; it was marked as resolved.

![Zabbix_8.png](./images/zabbix_8.png)

I can also visualise traffic on an interface of a network device. Below is `int g1/0` traffic graph.

![Zabbix_9.png](./images/zabbix_9.png)
