# omadaDeviceCli
This is used to create a script that can be added in the Omada controller to set DSCP for specific devices and ports, primarily for Dante..

![image](https://github.com/1024jon/omadaDeviceCli/assets/8061767/20b773a0-4509-4ddb-96a8-b692c578a55f)

## Dante ##
https://www.audinate.com/learning/faqs/how-does-dante-use-dscp-diffserv-priority-values-when-configuring-qos \
For the TPLink switches, it seems that only value 8 needs to have its priority increased, 46 and 56 are ok.
```
qos dscp-map 8 2
#SELECT PORT RANGES HERE - SEE BELOW
qos trust mode dscp

```

### Gigabit Ports ###

```
interface range gigabitEthernet 1/0/min#-max#
```

### MultiGig Ports ###

```
interface range two-gigabitEthernet 1/0/min#-max#
```

### 10G Ports ###

```
interface range ten-gigabitEthernet 1/0/min#-max#
```

#### Example ####
First we increase the DSCP value 8 to priority of 2\
Then we select the first 10 gigabit ports numbered 1-10 and set them to trust DSCP\
Then we select the 10G ports 49-52 and set them to trust DSCP\
This script then gets pasted into the device CLI in the Omada controller\
```
qos dscp-map 8 2
interface range gigabitEthernet 1/0/1-10
qos trust mode dscp
interface range ten-gigabitEthernet 1/0/49-52
qos trust mode dscp
```
