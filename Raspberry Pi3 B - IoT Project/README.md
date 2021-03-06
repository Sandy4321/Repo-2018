# To Do List: Raspberry Pi3 Model B for IoT Project

<b>1 - Plug and Play</b>  

<b>2 - Set up Amazon AWS IoT</b>  

https://docs.aws.amazon.com/iot/latest/developerguide/iot-sdk-setup.html  

Things/Manage/Register  
Details/Interact  
Note of the REST API endpoint  
Security/Create Certificate  
Directory called deviceSDK  
Download Key
Activate
Create new policy
Action field: iot:*  Resource ARN: *  
Create/Back  
Security/Certificates/Attach policy  
Certificates/Right-Click/Attach thing  

https://medium.com/@gomaketeam/connecting-raspberry-pi-zero-with-amazon-web-services-iot-part-i-working-with-aws-iot-caa8a0f6f91b  

<b>3 - Connect Raspberry to AWS IoT ( + Mosquitto - Broker MQQT)</b>  

https://medium.com/@gomaketeam/connecting-raspberry-pi-zero-with-amazon-web-services-iot-part-iii-installing-the-aws-iot-device-919de23f5642  

Installing the AWS IoT Device SDK  
Upload the Certificates and Keys to Your Device  
```
scp privkey.pem pi@raspberrypi.local:/home/pi
scp pubkey.pem pi@raspberrypi.local:/home/pi
scp crt.crt pi@raspberrypi.local:/home/pi
scp ca.pem pi@raspberrypi.local:/home/pi
```  

password: raspberry  
Download the AWS IoT Device SDK onto the Raspberry Pi  
ssh pi@raspberrypi.local  
```
wget https://s3.amazonaws.com/aws-iot-device-sdk-embedded-c/linux_mqtt_openssl-latest.tar  

mkdir /opt/devicesdk
mv linux_mqtt_openssl-latest.tar /opt/devicesdk
cd /opt/devicesdk
tar -xvf linux_mqtt_openssl-latest.tar  

mv /home/pi/privkey.pem /opt/devicesdk
mv /home/pi/pubkey.pem /opt/devicesdk
mv /home/pi/crt.crt /opt/devicesdk
mv /home/pi/ca.pem /opt/devicesdk  

sudo apt-get install -y libssl-dev

cd /opt/devicesdk/sample_apps/shadow_sample
nano aws_iot_config.h

#define AWS_IOT_MQTT_HOST “ENDPOINT.iot.us-east-1.amazonaws.com”
#define AWS_IOT_MQTT_PORT 8883
#define AWS_IOT_MQTT_CLIENT_ID “THING NAME”
#define AWS_IOT_MY_THING_NAME “THING NAME”
#define AWS_IOT_ROOT_CA_FILENAME “ca.pem”
#define AWS_IOT_CERTIFICATE_FILENAME “cert.crt”
#define AWS_IOT_PRIVATE_KEY_FILENAME “privkey.pem”
```  

Save  
```
make -f Makefile  
./shadow_sample
```  

Back to AWS
Shadow ARN  

(Mosquitto - MQTT)  

http://mosquitto.org/download/  

https://aws.amazon.com/pt/blogs/iot/how-to-bridge-mosquitto-mqtt-broker-to-aws-iot/  


<b>4 - Collect CPU Temperature (Python ?)</b>  

```
/opt/vc/bin/vcgencmd measure_temp

nano monitor-temp.py
```

```
import os
import time

def measure_temp():
        temp = os.popen("vcgencmd measure_temp").readline()
        return (temp.replace("temp=",""))

while True:
        print(measure_temp())
        time.sleep(1)
```  
CTRL X + Y  
```
python monitor-temp.py
```  

<b>5 - Monitor CPU Temperature</b>  

<b>6 - Send data to AWS IoT</b>  

<b>7 - Save data into Dynamo DB</b>  

https://docs.aws.amazon.com/iot/latest/developerguide/iot-ddb-rule.html  

<b>8 - Add sensor</b>  

<b>9 - Load saved Machine Learning model for anomaly detection</b>  

<b>10 - Dashboard</b>  

<img src=https://github.com/RubensZimbres/Repo-2018/blob/master/Raspberry%20Pi3%20B%20-%20IoT%20Project/Pictures/Raspberry%20Pi3.png>
