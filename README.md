
![awesomeklipper](https://github.com/TheVoronModder/Extra-Input-Shapers/assets/142328467/73336a9d-4fbf-4cd4-89a1-1693bf5a1230)

# Wondering how people have Shake&Tune "extra" results for Input Shaping? What is "SMOOTH" ya ya, well this is the place to help you.

## Keep in mind I am not advertising any sort of "tech support" whatsoever, and just like you I learn new things every day. The problem I have is once I set my eye on something I work tirelessly around the clock to get things working. With that being said there is probably an easier way to do this than the path I took however, my IS shake&tune works with smooth IS.

SO... Here we go:

## install dangerklipper using KIAUH

To do this, add the Danger Klipper repo to KIAUH's repo list and run the script with the following commands:

```bash
echo "DangerKlippers/danger-klipper" >> ~/kiauh/klipper_repos.txt
~/kiauh/kiauh.sh
```

then run KIAUH

```bash
~/kiauh/kiauh.sh
```

### From the KIAUH menu select:

6 ) Settings

1 ) Set custom Klipper repository

Select the number corresponding to DangerKlipper from the list shown

Select 'Y' to confirm replacing your existing Klipper install

Enter 'B' for back twice

'Q' to quit

```bash
sudo reboot
```

SSH back into your printers pi

we need to see what version of dangerklipper we installed.
to do this while in your ssh terminal send this:

```bash
cd ~/klipper/
```

now your in your klipper directory.

run this:

```bash
git branch
```

and then

```bash
git remote -v
```

if you get something like the image below it is simple to get the correct directory.

![dangerklipper version](https://github.com/TheVoronModder/Extra-Input-Shapers/assets/142328467/0b711abe-55be-44d6-8117-9e4b7585d162)

run these commands in the terminal:

```bash
git checkout bleeding-edge
```
```bash
sudo systemctl restart klipper
```

Re connect to your pi via ssh and verify you have bleeding-edge installed by running:

```bash
cd ~/klipper/
```
```bash
git branch
```

You should now see that your klipper version is now bleeding edge like the image below:

![dangerklipper version now bleeding edge](https://github.com/TheVoronModder/Extra-Input-Shapers/assets/142328467/d885768e-91e9-4c57-8329-c549e44fb43c)

### Now the fun part - kind of..... reflashing your MCU!

So, now we need to re-build and re-compile the firmware we did originally but this time were going to add 1 NEW option that was never there before....

the process is the same for setting any MCU up for Klipper regardless of what you have...

ssh back into your pi if you left or closed it out.

You should be in 
```bash
~/klipper/
```
directory.

```bash
make menuconfig
```

## from here follow the recipe for your MCU but CHECK "High-precision stepping support (slow)"

![danger klipper mcu bro](https://github.com/TheVoronModder/Extra-Input-Shapers/assets/142328467/97bb145a-76a5-4759-b360-c23606d18d49)

hit "Q" to quit, "Y" for yes, we want to save. then

```bash
make clean
```

```bash
make
```

Now to flash.....

we need to find the correct serial by-id...

```bash
ls /dev/serial/by-id/*
```

The output should look similar to this:

```/dev/serial/by-id/usb-Klipper_stm32f042x6_010001000C123456789123-if00```

with this serial path you need to perform the flash command:

```bash
sudo systemctl stop klipper
make flash FLASH_DEVICE=<serial path to the board>
sudo systemctl start klipper
```

## for some reason if this does not work you can always use an sd card by copying the klippy.bin file and go that route. 

# this is the time to reflash the RaspberryPi! yay?

okay, seriously though, this part can be daunting for newbies, in all honesty its quite smiple. 

ssh back into your pi. execute the following commands:

```bash
cd ~/klipper/
make menuconfig
```

Then MAKE SURE YOU CHOOSE THE CORRECT THING HERE:






