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

![image](BinwalkCapture.png)

Your output will not match this exactly (this is a `binwalk` analysis of the current NAND Flash in my Console which is heavily modified). What's important is the address of the **squashfs** filesystem which is 16777216 (I'm assuming this address will be the same for anyone's MyArcade Console), we'll need this later. The `binwalk` program will extract all files into a `_nand_dump_bin.extracted` folder (your extracted files will not look like mine since I have modified my console's filesystem memory). 

![image](ExtractedBinariesCapture.png)

Change directory into the `squashfs-root`. We should see a directory similar to this.

![image](ConsoleFilesystemCapture.png)

You can now dive into the filesystem and check what programs are available (`usr/bin` has some interesting programs). For this tutotiral we are interested in the `usr/lib/libretro` folder. This contains the emulators and games available to the console. You should see the following emulators

1. `fbalpha_libretro.so`
2. `mame2016_libretro.so`

If you look in the `games` folder (this folder may not exist and have been something I added during modding) you should see `fzip` and `mzip`. I know `fzip` contains Contra ROMs for the **fbalpha** emulator which implies that `mzip` contains Contra ROMs for the **mame2016** emulator.