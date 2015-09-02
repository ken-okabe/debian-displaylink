# debian-displaylink

http://www.displaylink.org/forum/showthread.php?t=64041

http://www.displaylink.org/forum/showthread.php?t=64043



run the displaylink-driver-1.0.138.run file with the --keep --noexec options to unpack the files

 Edit the line with SYSTEMINITDAEMON= to be SYSTEMINITDAEMON=systemd

detect_distro()
{
  if which lsb_release >/dev/null; then
    local R=$(lsb_release -d -s)
    echo "Distribution discovered: $R" 
    SYSTEMINITDAEMON=systemd
   
  else
    echo "WARNING: Unknown distribution, assuming defaults - this may fail." >&2
  fi
}


sudo ./displaylink-installer.sh install




The installer script is looking for
Code:
/lib/modules/$(uname -r)/build/Kbuild
to ensure that kernel headers are available for a running kernel. Ensure the headers are indeed installed, then change or remove the line to match files available on Debian.


/lib/modules/3.16.0-4-amd64/build# ln -sf Makefile Kbuild
linking the Makefile to Kbuild seemed to allow me to install the drivers without error.



lsusb
dmesg | grep -i display
lsmod | grep evdi

systemctl status display-manager.service
systemctl status displaylink.service

xrandr --listproviders
xrandr --setprovideroutputsource 1 0
