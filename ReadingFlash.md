# Reading From Flash Memory

I highly recommend reading the [article](https://trustedsec.com/blog/hacking-the-my-arcade-contra-pocket-player-part-i) I mentioned in the introduction. It does a much better job explaining the inner workings of the MyArcade Contra Console and the process of reading flash memory. This guide will be pulling most of its information from that article.

## Enabling Mask ROM Mode
A cool property of some Rockchip chips is that we can enable its recovery mode by sending the Volume Up (as in sound volume) signal to the chip during its boot sequence. Since the MyArcade Contra Console uses a RK3128 (Rockchip 3218) we can enable its recovery mode by holding down the **Volume Up** button during the boot sequence of the console. This will put the chip in **Mask ROM Mode** allowing us to ask it for Flash memory.

## Reading the Flash
Now that the console is in **Mask ROM Mode** we can ask the **RK3128** very nicely for its flash memory. You will need to install the `rkflashtool` application to read/write the flash memory for the conosle. You will also need a USB cable to connect your PC to the Console through its micro USB female port.

To get a dump of the flash memory we'll use the command:


```bash
sudo ./rkflashtool r 0 262144 > ~/Desktop/nand_dumps/nand_dump.bin
```
(I am copying this command from this [article](https://trustedsec.com/blog/hacking-the-my-arcade-contra-pocket-player-part-i))

We have now reached the end of information from the [article](https://trustedsec.com/blog/hacking-the-my-arcade-contra-pocket-player-part-i) and everythign going forwawrd will be my findings from messing around with this console.

Now that we have a dump of the entire flash memory, we find the part that contains the filesystem the console uses. We can use a tool like `binwalk` to analyze and separate the **nand_dump.bin** binary.

```bash
binwalk -e ~/Desktop/nand_dumps/nand_dump.bin
```