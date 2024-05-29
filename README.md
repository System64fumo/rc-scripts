# rc-scripts
This repository holds the rc scripts that i use on my systems<br>

# Installation
To install and use these scripts on your system you need to do the following: <br>
1. `mkdir /opt/busybox`
2. Download busybox and put it in /opt/busybox
3. Install busybox by either symlinking or running `/opt/busybox/busybox --install -s /opt/busybox/`
4. `git clone https://github.com/System64fumo/rc-scripts`
5. `sudo mv ./rc-scripts/rc.d /etc/rc.d`
6. `sudo mv ./rc-scripts/inittab /etc/inittab`
7. `sudo rm /bin/{init,poweroff,reboot}`
8. `sudo ln -s /opt/busybox/init /bin/init`
9. `sudo ln -s /opt/busybox/poweroff /bin/poweroff`
10. `sudo ln -s /opt/busybox/reboot /bin/reboot`

Do note: After following the installation guide,<br>
You will not be able to reboot your system normally for the first time (Since we replaced the original poweroff file)<br>
Also any updates to your init system of choice will restore the original init,<br>
So add your init system to your package manager's ignore/block list.

# Configuration and usage
To manually start or stop a service, Run the `service` script.<br>
Example: `sudo /etc/rc.d/script start sshd`<br>

To configure which services load when you boot the system up, <br>
Edit `/etc/rc.d/init`.<br>

To configure what happens when you shut the system down, <br>
Edit `/etc/rc.d/shutdown`.<br>

To configure service settings, (Such as zram size, Network details, ect..)<br>
Edit `/etc/rc.d/config`.<br>

To configure ttys or autologin, (The default autologin is for root on tty1)<br>
Edit `/etc/inittab`.

# Additional information
By default the service loader will use busybox,<br>
Uncomment the export line in `/etc/rc.d/service` to use native system bins if you wish.<br>

The splash screen configuration `/etc/rc.d/splash/fbsplash.ini` assumes your monitor resolution is 1080p.<br>

> [!IMPORTANT]
> The default configuration assumes a lot, Such as:<br>
> Running on a non systemd based distro<br>
> Connected via ethernet on eth0 with a static ip addr<br>
> Using pipewire for audio<br>
> Please change it to match your system and your needs.<br>

> [!NOTE]
> Some services should not run as the root user (Such as audio for example)<br>
> You can use `su` to start them automatically in `/etc/rc.d/init`<br>


# Why do any of this? And why busybox?
The following answers are based on my opinion, Feel free to disagree.<br>
I personally like the way sysvinit style init systems work (Shell script based init systems)<br>
I find it easier to configure and do everything i want this way too<br>
The speed and performance of existing init systems did not satisfy me.<br>

As for the busybox question, Honestly?<br>
I just wanted to mess around with busybox a while back and tried it's init system, So it kinda stuck<br>
I am fully aware that busybox is not exactly the best thing out there,<br>
However i'm too lazy to switch to something else<br>
