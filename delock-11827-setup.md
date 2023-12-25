# New Delock 11827 device in my environment

When I get a new 11827 device, I had to set it up manually in the past.

Having a spare Raspberry Pi, I was able to connect to the default Wifi of the Delock device.

This will only work if 192.168.4.0/24 is unused so far on the Pi.

On the Raspberry Pi:

Run `iwlist scan | grep delock-`

Note the 4-digit number from the output.
Example: `ESSID:"delock-1234"`

A file delock-connect.conf. Change the ssid to match the ssid from the Delock device.

```
network={
	ssid="delock-1234"
	key_mgmt=NONE
}
````

Connect to Delock device.

`wpa_supplicant -i wlan0 -c delock-connect.conf -Dwext`

The delock device is pingable now.
`ping 192.168.4.1 -c 3`

Run commands to get hostname and Mac address:

```
curl "192.168.4.1/cm?cmnd=Status%205" | jq -r '.StatusNET.Mac'
curl "192.168.4.1/cm?cmnd=Status%205" | jq -r '.StatusNET.Hostname'
```

Hostname should be the same as SSID from scan command.

Set Home SSID, password, mqtt server, and mqtt topic:

`curl "192.168.4.1/cm?cmnd=Backlog%20SSID1%20nameofyourssid%3B%20Password1%20yourpassword%3B%20MqttHost%yourmqtthostname%3B%20Topic%20delock-1234"`

Using Backlog command, the device will restart only once.

Terminate wpa_supplicant:

```
fg
<Ctrl+C>
```
