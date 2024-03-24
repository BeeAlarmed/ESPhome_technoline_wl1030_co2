# ESPhome_technoline_wl1030_co2
Integrate the Co2 readings from a Techno Line WL 1030 into ESPhome / Home Assistant

<img src="/images/IMG_20240324_134845_430.jpg" width="280px">

The Co2 sensor used by the Technoline WL 1030 seems to be a *Cubic NDIR CO2 Sensor Module CM1106-C*. This sensor has a PWM output, that can be used by an ESP to measure the Co2 readings. 

This solution does not read any other values than the Co2!

## Adding an ESP to the Techno Line

- Open the Techno Line (There is a hidden screw under the stand)
- Connect *VIN* from the Co2 to ESP VIN/BAT/5V
- Connect *GND* from the Co2 to ESP GND
- Connect *PWM* from the Co2 to ESP input pin (I used GPIO14)
- Solder a Pull-Up of 5k-10k between *VIN* and *PWM* (I'm not 100% this is neede, but the datasheet mentions that you need it while using an oscilloscope)


## Esp Home configuration


```yaml
...
    
sensor:
  - platform: pulse_width
    pin: GPIO14
    name: Co2
    update_interval: 30s
    filters: 
      - lambda: return (x-0.002) * 5000;

    unit_of_measurement: "ppm"
    icon: "mdi:molecule-co2"
    device_class: "carbon_dioxide"
    state_class: "measurement"
    accuracy_decimals: 0


```

Example output, taken from ESP home in Home Assistant
```bash
[13:57:06][D][sensor:093]: 'Co2': Sending state 793.76996 ppm with 0 decimals of accuracy
[13:57:36][C][pulse_width:026]: 'Co2' - Got pulse width 0.172 s
[13:57:36][D][sensor:093]: 'Co2': Sending state 849.76495 ppm with 0 decimals of accuracy
[13:58:06][C][pulse_width:026]: 'Co2' - Got pulse width 0.179 s
[13:58:06][D][sensor:093]: 'Co2': Sending state 882.71002 ppm with 0 decimals of accuracy
[13:58:36][C][pulse_width:026]: 'Co2' - Got pulse width 0.165 s
[13:58:36][D][sensor:093]: 'Co2': Sending state 812.76001 ppm with 0 decimals of accuracy
[13:59:06][C][pulse_width:026]: 'Co2' - Got pulse width 0.155 s
[13:59:06][D][sensor:093]: 'Co2': Sending state 762.74500 ppm with 0 decimals of accuracy
[13:59:36][C][pulse_width:026]: 'Co2' - Got pulse width 0.155 s
[13:59:36][D][sensor:093]: 'Co2': Sending state 763.74506 ppm with 0 decimals of accuracy
[14:00:06][C][pulse_width:026]: 'Co2' - Got pulse width 0.168 s
[14:00:06][D][sensor:093]: 'Co2': Sending state 828.73004 ppm with 0 decimals of accuracy
[14:00:36][C][pulse_width:026]: 'Co2' - Got pulse width 0.168 s
[14:00:36][D][sensor:093]: 'Co2': Sending state 831.88501 ppm with 0 decimals of accuracy
[14:01:06][C][pulse_width:026]: 'Co2' - Got pulse width 0.155 s
[14:01:06][D][sensor:093]: 'Co2': Sending state 764.94000 ppm with 0 decimals of accuracy
[14:01:36][C][pulse_width:026]: 'Co2' - Got pulse width 0.145 s
[14:01:36][D][sensor:093]: 'Co2': Sending state 716.89502 ppm with 0 decimals of accuracy
[14:02:06][C][pulse_width:026]: 'Co2' - Got pulse width 0.141 s
[14:02:06][D][sensor:093]: 'Co2': Sending state 692.81995 ppm with 0 decimals of accuracy
[14:02:36][C][pulse_width:026]: 'Co2' - Got pulse width 0.143 s
[14:02:36][D][sensor:093]: 'Co2': Sending state 705.92505 ppm with 0 decimals of accuracy
[14:03:06][C][pulse_width:026]: 'Co2' - Got pulse width 0.141 s
[14:03:06][D][sensor:093]: 'Co2': Sending state 695.86005 ppm with 0 decimals of accuracy
```

## Images

<div style="width:640px">
	<img src="/images/IMG_20240324_131228_758.jpg" height="240px">
	<img src="/images/IMG_20240324_130715_167.jpg" height="240px">
	<img src="/images/IMG_20240324_131304_146.jpg" height="240px">
	<img src="/images/IMG_20240324_132217_328.jpg" height="240px">
	<img src="/images/IMG_20240324_133421_561.jpg" height="240px">
	
</div>
