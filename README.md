# Rpi-weather-monitor
### Raspberry Pi powered weather monitor with Bosch BME280 sensor
![alt text](https://github.com/Ollisyr/Rpi-weather-monitor/blob/master/RPi_WeatherApp.png "Mobile view")

### Connecting Hardware
This weather application use BME280 sensor from  Bosch Sensortec and the official datasheet includes all the technical details:
https://ae-bst.resource.bosch.com/media/_tech/media/datasheets/BST-BME280_DS001-12.pdf

| Sensor PCB        | Decription           | GPIO header pins  |
| ------------- |:-------------:| :-----:|
| VCC      | 3.3 V | P1-01 |
| GND      | Ground     |   P1-06 |
| SCL | I2C SCL      |   P1-05 |
| SDA | 	I2C SDA      |   P1-03 |

Remember enable the I2C interface on the Raspberry Pi as it is not enabled by default. Also check locale and timezone and change if necessary.
In order to have a web server run automatically when the Pi boots edit rc.local: <br>
`sudo nano /etc/rc.local` <br>
And add following line: <br>
`python /home/pi/weather.py & ` <br>
In order to have a scheduled tasks run edit crontab: <br>
` sudo nano /etc/crontab ` <br>
And add following lines: <br>
` 0  *    * * *   root    sudo python /home/pi/bme280.py ` <br>
` 5,15,25,35,45,55 * * * *   root    sudo python /home/pi/minmax.py ` <br>
You can also add initminmax.py to crontab, if you want periodically reset stored minimum and maximum values.<br>
