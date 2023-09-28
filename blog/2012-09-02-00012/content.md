Ever since I got my [MacAir late last year](https://hectorcorrea.com/blog/ruby-development-on-the-mac-os-x/15) I've been having **issues copying files from my Mac to my external storage device**. My external storage device is a Buffalo HD-CELU2 DriveStation that can be accessed as a standard USB drive or as network attached storage (NAS.) I've been using this device as a NAS from my Windows computers for a couple of years with no problems but my Mac refused to work smoothly with it.

On my Mac I was able to read files from the NAS but I couldn't write files to it. When I tried to copy files to the NAS I got the dreaded and cryptic "Finder Error -36". There are several people reporting similar issues when using a NAS from their Macs and it took me several months before I found a solution that worked for me. Below is an example of the error that Finder will throw when I tried to copy a file (SamplePDF.pdf) to my NAS (hd-celu2-fce7).

![Finder error -36 on NAS](https://hectorcorrea.com/images/nas_finder_error_36.png)


## The clues

One of the things that I noticed in dealing with this issue was that the Buffalo DriveStation worked smoothly when I connected it directly to my Mac's USB port (rather than accessing it through the network.) When I used the device through the USB port I was able to read and write files with no problems. This lead me to believe that the problem was somehow related to the way the Mac was accessing the device through the network rather than the drive itself. If the drive was formatted in a way that was incompatible with the Mac I would have the same problems no matter how I accessed it.

Here is a description of the issues that I noticed when I connected to the Buffalo DriveStation as a network drive:

* My Mac computer can read files from the NAS with no problem.
* My Mac cannot write files from the NAS. I get the infamous "Finder Error -36".
* My Windows computer can read from the NAS and write files to it with no problem

Although I was able to read and write with no problems if I connected to the device through my USB port, using it this way defeated the purpose of having a NAS in the first place. I wanted to be able to connect to the device through my wireless network at home rather than having to drag the darn thing with me around the house.

I also noticed that the problem was not exclusive to Finder, I would also get an error when I tried to copy files to my NAS through the Terminal as shown in the following screenshot. In Terminal I was able to work around this problem by using `-X` switch on the copy command as shown in the following screenshot. Notice how the first copy failed but the second succeeded. The [-X switch](http://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man1/cp.1.html) prevents the copy command from copying Extended Attributes or resource forks.

![Terminal error on NAS](https://hectorcorrea.com/images/nas_terminal_error.png)


## The solution 

I found the solution to my problem at macwindows.com under [TIP: Another take on smb.config fix for -36 file sharing error: edit nsmb.conf for "streams=no"](http://www.macwindows.com/snowleopard-filesharing.html#012510e). You basically need to edit a configuration file to tell the Mac not to use streams when connecting to the NAS. In particular you need to add the following two lines to the `/etc/nsmb.conf` file:

```
[default]
[streams=no]
```

If the file does not exist on your machine (it didn't on mine) you will need to create it. Editing/creating this file is bit tricky since you need elevated permissions. The macwindows.com link has detailed steps on how to do this.

The aforementioned lines will tell the Mac OS X to [turn off the use of NTFS streams](http://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man5/nsmb.conf.5.html) when connecting via SMB to a device.

As it turns out, when the Mac connects to the Buffalo DriveStation through the network it uses a protocol called SMB. That's the reason you see "SMB://somename/somepath" in Finder when you connect to an external storage device. One of the things that I learned on the macwindows.com page is that SMB is a protocol to access drive and other devices (just like FTP or HTTP) and file `nsmb.conf` *configures the SMB client that comes with the Mac* (see [SMB vs. Samba, and what Apple uses for file sharing](http://www.macwindows.com/snowleopard-filesharing.html#011011e).)


## An even simpler solution

I found an even *simpler way to turn off streams* in this article on Apple's web site: [Mac OS X v10.5, v10.6: About named streams on SMB-mounted NAS, Mac OS X, and Windows servers; "-36" or "-50" alerts may appear](http://support.apple.com/kb/HT4017). It turns out you can just create file on the device where you want to turn streams off by using a command like this:

```
touch /Volumes/SharedNAS/.com.apple.smb.streams.off 
```

where `SharedNAS` is the name of your shared device. The Apple article also includes a great explanation of what the heck it means to "turn off streams" when connecting to an external device through SMB.


## Are there any side effects?

I've been using my NAS device from my Mac with no problems for almost two weeks since I turned off streams with the solutions in this blog post. I can now read from and write to the NAS from both my Mac and Windows computers. The only side effect that I've seen so far is that, since streams are turned off, the Mac OS X creates two files on the NAS for every file that I copy to it. These double files are only visible when I access the NAS device from my Windows computer.

The aforementioned [article on the Apple web site](http://support.apple.com/kb/HT4017) indicates that "named streams are used to store Mac OS X extended attributes and can be leveraged to avoid using AppleDouble files to store the data fork and the resource fork of legacy Mac files" so it makes sense that (1) the files are now being created since we turned off streams and (2) these double files are visible from a non OS X operating system.

The following screenshots show how the folder with the SamplePDF file is displayed in Finder and in Windows Explorer

![NAS file from OS X](https://hectorcorrea.com/images/nas_mac.png)

![NAS file from Windows](https://hectorcorrea.com/images/nas_windows.jpg)

This double file nuance is not a big deal for me specially given that for many months I couldn't even write files to my NAS from my Mac.