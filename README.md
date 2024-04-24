
![awesomeklipper](https://github.com/TheVoronModder/Extra-Input-Shapers/assets/142328467/73336a9d-4fbf-4cd4-89a1-1693bf5a1230)

# Wondering how people have Shake&Tune "extra" results for Input Shaping? What is "SMOOTH" ya ya, well this is the place to help you.

## Keep in mind I am not advertising any sort of "tech support" whatsoever, and just like you I learn new things every day. The problem I have is once I set my eye on something I work tirelessly around the clock to get things working. With that being said there is probably an easier way to do this than the path I took however, my IS shake&tune works with smooth IS.

SO... Here we go:

## install dangerklipper using KIAUH

To do this, add the Danger Klipper repo to KIAUH's repo list and run the script with the following commands:

```
echo "DangerKlippers/danger-klipper" >> ~/kiauh/klipper_repos.txt
~/kiauh/kiauh.sh
```

then run KIAUH

```
~/kiauh/kiauh.sh
```

### From the KIAUH menu select:

6 ) Settings

1 ) Set custom Klipper repository

Select the number corresponding to DangerKlipper from the list shown

Select 'Y' to confirm replacing your existing Klipper install

Enter 'B' for back twice

'Q' to quit

```
sudo reboot
```

SSH back into your printers pi

we need to see what version of dangerklipper we installed.
to do this while in your ssh terminal send this:

```
cd ~/klipper/
```

now your in your klipper directory.

run this:

```
git branch
```

and then

```
git remote -v
```

if you get something like the image below it is simple to get the correct directory.

![dangerklipper version](https://github.com/TheVoronModder/Extra-Input-Shapers/assets/142328467/0b711abe-55be-44d6-8117-9e4b7585d162)

run these commands in the terminal:

```
git checkout bleeding-edge
```
```
sudo systemctl restart klipper
```

Re connect to your pi via ssh and verify you have bleeding-edge installed by running:

```cd ~/klipper/```
```git branch```

You should now see that your klipper version is now bleeding edge like the image below:

![dangerklipper version now bleeding edge](https://github.com/TheVoronModder/Extra-Input-Shapers/assets/142328467/d885768e-91e9-4c57-8329-c549e44fb43c)

### Now the fun part - kind of..... reflashing your MCU!

So, now we need to re-build and re-compile the firmware we did originally but this time were going to add 1 NEW option that was never there before....

the process is the same for setting any MCU up for Klipper regardless of what you have...

ssh back into your pi if you left or closed it out.

You should be in 
```
~/klipper/
```
directory.

```
make menuconfig
```


from here follow the recipe for your MCU but CHECK "High-precision stepping support (slow)"

![danger klipper mcu bro](https://github.com/TheVoronModder/Extra-Input-Shapers/assets/142328467/97bb145a-76a5-4759-b360-c23606d18d49)



