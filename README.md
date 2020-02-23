# ipad_as_2nd_monitor
Use ipad or android tablet as your 2nd Monitor with your Linux Laptop/PC

Everytime I am travelling and If I want to work on my laptop it's hard to multitask because you normally used to with dual monitor at home or at work, and while you travel normally you have only laptop and tablet. I have been googling about solution to use my ipad at dual monitor without any extra accesories, which led me to [__Aditya's__](http://www.adityavaidya.com/2015/03/ipad-as-2nd-monitor-now-on-linux.html) post. With that I was able to achive what I wanted but there was some manual steps involved, So I decided to make single script which takes care of running multiple scripts.  
  
  
### Demo
![Demo](ezgif.com-video-to-gif.gif)
  
## Things you need:
- ipad/Android tablet with VNC Viewer(I'm using ipad with VNC Viewer app)  
- Linux Desktop(I'm using ElementaryOS Which is built on Ubuntu 18.04)  
  
  
### Before you start:  

I am using X11VNC in my setup and x11vnc droped `-multiptr` option but you can follow below steps to enable it: 
```
git clone https://github.com/LibVNC/x11vnc.git
cd x11vnc
sudo apt-get install libvncserver-dev
./autogen.sh
./configure
make
sudo make install
```
  
  
Now based on your __GPU__ you've to create configuration file at: /usr/share/X11/xorg.conf.d/ in my case I've created '20-intel.conf' with below parameters:
  
  
`/usr/share/X11/xorg.conf.d/20-intel.conf`
  
```
Section "Device"  
         Identifier "intelgpu0"  
         Driver "intel"  
         Option "VirtualHeads" "2"
EndSection
```
   
  
Once all setup just simply download [__ipad_monitor.sh__](https://github.com/rajsardhara/ipad_as_2nd_monitor/blob/master/ipad_monitor.sh) and run:

`./ipad_monitor.sh -r` '__-r__' will create additional display on right side of laptop.
```
./ipad_monitor.sh -r    # or --right. Second screen appears right to the primary monitor.
./ipad_monitor.sh -l    # or --left
./ipad_monitor.sh -a    # or --above
./ipad_monitor.sh -b    # or --below
./ipad_monitor.sh -r -h    # or --hidpi. HiDPI mode. It doubles the resolution.
./ipad_monitor.sh -r -p    # or --portrait. Portrait mode.
./ipad_monitor.sh -l -p -h    # Left, portrait mode, and HiDPI mode.
```

Then get ip of your laptop using __ifconfig__ and connect from ipad using VNC client. 

__Offline Use :__ _You can use offline by creating wifi hotspot on your laptop._
