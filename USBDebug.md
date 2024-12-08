# USB Debug Mode

Currently, our only way to control the console is by providing it commands in the `/etc/init.d/S50ui` file. What would be really nice is to have an interactive terminal on the console so that we can send commands to the console from a separate device. This will also make debugging issues waaayyyy easier.

To do this we will need to modify the device tree within the flash memory. We need to swtich the `dr_mode` property of the `usb@10180000` from `host` to `otg` (you may also be able to switch it to `peripheral` however I haven't tried this yet). If you've read the [Setup Serial Terminal](SetupSerialTerminal.md) this process will be very similar.

Search for `usb@10180000`, however the first match will probably not be what we want. We want to find the `usb@10180000` device tree entry that contains the string `host`
![image](web/FindOTGCapture.png)

We now need to overwrite `host` with `otg` and replace the **t** in hos**t** with a null byte (0x00)
![image](web/EnableOTGCapture.png)

Now we'll install the `adb` program (`sudo apt install adb` on Linux).


AFter connecting the conosle we can list connected `adb` devices like so:

`adb devices`

![image](web/ListADBDevices.png)

We can now initiate the debug terminal using `adb`:

`adb shell`

![image](web/ADBShellCapture.png)

<div style="display: flex; justify-content: space-between;">
  <a href="README.md" style="text-decoration: none; padding: 10px 20px; background-color: #007BFF; color: white; border-radius: 5px;">&larr; Table of Contents</a>
  <a href="WritingFlash.md" style="text-decoration: none; padding: 10px 20px; background-color: #007BFF; color: white; border-radius: 5px;">Setup Serial Terminal &rarr;</a>
</div>