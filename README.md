# IoT_Mini_Project_1 
 **Group-5: Md Mia, Md Esti, Abdullah Chaudhry**



##  Introduction ##

We want to measure temperature, pressure and luminosity from the sensors. 

Sensors:  
1. Temperature Sensor (LPS331AP): It measures temperature in Celcius
2.  Pressure Sensor (LPS331AP): Is measures atmospheric pressure in hPa.
3.  Luminosity (Light) Sensor (ISL29020): It measures ambient light intensity in lux.

IOT_LAB M3 board contains all these sensors. 

The whole setup is done by 'RIOT OS' on 'IoT-LAB'
## Setup ##
To be able to connect to an IoT-LAB site server, you have to add your SSH key to your user account.
 1.  Generate a pair of SSH keys from the VS Code Terminal:
```
rm -f ~/.ssh/id_rsa* && ssh-keygen -q -N "" -C iot-lab-training -f ~/.ssh/id_rsa
```
 2.  Get the SSH public key by running the following cell:
```
iotlab-auth --add-ssh-key
```
 3.  Copy the output of the previous command and add it as authorized SSH key for your account:  
    [https://www.iot-lab.info/testbed/account](https://www.iot-lab.info/testbed/account)  (SSH Keys tab)
    
 4. Verify the setup by connecting to the Lyon's server site running the
    following command in the Terminal:

```
ssh $IOTLAB_LOGIN@lyon.iot-lab.info
```    

    
## Experiment: Sensors ##
To run the application the most important thing is to follow the path. For this application, the path is like this. If you change the path remember to fix this. 

RIOTBASE ?= $(CURDIR)/../../RIOT

First you have to go to the Sensors directory

Then open a terminal and go to the folder containing the main.c and make file.

Select an environment with the following command. We have always chosen the grenoble site. 
```
env SITE=grenoble
```
Submit an experiment using the following command:
```
iotlab-experiment submit -n "iot_sensors_data" -d 20 -l 1,archi=m3:at86rf231+site=grenoble
```
Here the experiment will last 20 minutes. It can be modified. Similarly, the site can be changed by modifying the value of the SITE variable in the command. 

After that we have to wait to see the 'Running' status.

Then write the following command:
```
iotlab-experiment wait --timeout 30 --cancel-on-timeout

```
Get the experiment nodes list:
```
iotlab-experiment --jmespath="items[*].network_address | sort(@)" get --nodes

```
Now put this command
```
source /opt/riot.source

```
Build and flash using the following command

```
make IOTLAB_NODE=auto flash
```

To see the results, go to the "My experiments" section on Iot-LAB.
You will get the following result:





## Experiment: COAP ##

Secondly, we tried to communicate between two IOT LAB nodes using the Coap protocol.


Now first you have to come out from the Sensors directory and have to go the Coap directory. 

Open two terminals in VS Code. 

Select an environment with the following command. We have always chosen the grenoble site. 
```
env SITE=grenoble
```
Write the following command
```
source /opt/riot.source
```
Now write the following command
```
make
```
Submit the first experiment using the following command:
```
iotlab-experiment submit -n Coap -d 60 -l grenoble,m3,3,./bin/iotlab-m3/Coap.elf
```
Submit the second experiment using the following command:
```

iotlab-experiment submit -n Coap -d 60 -l grenoble,m3,4,./bin/iotlab-m3/Coap.elf
```
Wait for the experiment to be in the Running state
```
iotlab-experiment wait --timeout 30 --cancel-on-timeout
```
Get the experiment nodes list:
```
iotlab-experiment --jmespath="items[*].network_address | sort(@)" get --nodes
```

In the first terminal, which we will now call the coap server, you can type the following command: 
```
nc m3-4 20000
```
After that press enter and then type: 

```
ifconfig
```
you will get the IP V6 address of the coap server.

You can also use the  coap info command to know the port in which it is listening :

```
coap info
```
The server listens usually on port 5683. 

Now go to the second terminal.
Enter the following command to set up the client. 
```
nc m3-3 20000
```
You can then test communication with the second node, the coap client.
 by typing the following command in the second terminal followed by the server's IPV6 address. You will get this address from the first terminal. 
```
ping <IPV6 Address>
```

To check wheather the client is properly working or not type the following command to retrieve  the temperature values from the sensor.
```
coap get <ipv6> : 5683 /temperature
```
Remember to replace ```<ipv6>``` by the IP V6 adress of the server.


Now you can see the temperature properly. That means, the two servers are communicating properly. 




## Demonstration video ##

[Demonstration video]
