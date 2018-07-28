# upm-rotary-mqtt-remote
<p>The purpose of this application is to evaluate the performance of MQTT and Websockets for viewing live sensor data remotely. The container inside of <b>mqtt-server</b> will be deployed on your remote server. The container inside of <b>mqtt-client</b> will be run on your local UpSquared device. </p>

<h2>Getting Started:</h2>

![upSquared](https://github.com/mdrolet01/upm-rotary-mqtt-remote/blob/master/images/upSquared.jpg)<br>
First, you will need an UpSquared Board with the GROVE kit
Connect the GROVEPI shield to the board
Plug in the Rotary sensor to A0 (Analog pin 0)
Make sure docker engine is installed on your computer

<h2>Instructions:</h2>
Since our Docker containers need to access the ports on your local device, you will have to kill any processes using ports 1883 (MQTT), 8000 (Web Server), and 27017 (MongoDB). You can accomplish this with the following commands:

    sudo service mosquitto stop
    sudo service mongod stop
*Note**: *The command for stopping a web server may vary. Make sure to kill any processes using port 8000.*

You are now ready to begin building the containers. Enter the following commands in your shell:
<h3>Local Device:</h3>

    git clone https://github.com/mdrolet01/upm-rotary-mqtt-remote.git
    cd mqtt-client
    docker build . -t mqttpy
    
Edit the app.py file inside of <b>mqtt-client</b> by changing the line broker='remote_ip_address' to reflect the correct IP address of your remote server (Ex. broker='0.0.0.0' if your remote IP is 0.0.0.0). Now run the container by typing:

    docker-compose up

<h3>Remote Device:</h3>

    git clone https://github.com/mdrolet01/upm-rotary-mqtt-remote.git
    cd mqtt-server
    docker build . -t nws
    docker-compose up


<h2>Viewing the Data</h2>
To view the live sensor data, open a browser with the URL of your remote server using port 8000 (Ex. remote_server_url:8000). You should see the following graph of your Rotary Sensor:

![sensorData](https://github.com/mdrolet01/upm-rotary-mqtt-remote/blob/master/images/sensorData.png)
<br>
