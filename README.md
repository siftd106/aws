# AWS IoT support for Mongoose OS

This Mongoose OS library allows your device to talk to Amazon AWS IoT service.
It implements device shadow API in both C/C++ and JavaScript, allowing a
developer to quickly prototype the device logic in JS before jumping to the
C/C++ implementation.

`mos` tool provides `mos aws-iot-setup` command for quick AWS IoT provisioning.
Take a look at the example video that shows how to implement Internet button
functionality in less than 2 minutes:

<iframe src="https://www.youtube.com/embed/nA3tGsSFngc"
  width="560" height="315"  frameborder="0" allowfullscreen></iframe>

`mos aws-iot-setup` command performs the certificate management for you, and
onboard your device on AWS IoT cloud. If your device has an
[Atmel ECC508A](http://www.atmel.com/devices/ATECC508A.aspx) secure element
attached, then Mongoose Firmware will use ECC508A chip for TLS handshake
and keep your credentials secure.

## How to use this library

In your Mongoose OS app, edit `mos.yml` file and add a reference to this
library. See an [example app](https://github.com/mongoose-os-apps/blynk)
that does that.

## Remote management via AWS IoT

If you're using Bash shell, you can use this alias to talk to your
device interactively via AWS IoT:

<pre class="command-line language-bash" data-user="chris" data-host="localhost" data-output="3-100"><code>alias mos1="mos --cert-file $(mos config-get mqtt.ssl_cert) --key-file $(mos config-get mqtt.ssl_key) --port mqtts://$(mos config-get mqtt.server)/$(mos config-get device.id)"
mos1 ls -l
init.js 330
index.html 250
...</code></pre>

For more in-depth explanation, see
[Secure remote device management with Mongoose OS](https://mongoose-os.com/blog/secure-remote-device-management-with-mongoose-os-and-aws-iot-for-esp32-esp8266-ti-cc3200-stm32/)
blog post.

## Device configuration

This library adds an `aws` configuration section to the device:

```json
"aws": {
  "shadow": {
    "thing_name": ""
  }
}
```
If `aws.shadow.thing_name` is left empty, then the provisioned device will
use a `device.id`, which is by default `<architecture>_<mac_address>`.
For example, a newly provisioned ESP32 board might have `esp32_C513DA` thing name.


## Other examples


### AWS device shadow tutorial
<iframe src="https://www.youtube.com/embed/H8w0_pWu0ak"
  width="560" height="315" frameborder="0" allowfullscreen></iframe>
