# runvncserver
Shell script to run TigerVNC server 

## Prerequisites
TigerVNC server installed (tigervnc-scraping-server on debian)  

The script checks, if you have already a .vnc Directory in your home ($HOME). You have to set a vnc password with the "vncpasswd" command, this will result a ~/.vnc/passwd file. However, on debian, the default TigerVNC server binary for scraping is at /usr/bin/x0vncserver (where x0 means the Xsession at display :0).

## Features
The script runs in the background, creates a logfile (default ~/.vnc/logfile), where it stores the actual x0vncserver logging information. There is also a pid file, default ~/.vnc/${HOSTNAME}${DISPLAY}.pid where the process id is stored.

The default port is for the :0 display 5900. If you want to change it, just edit VNCPORT="5900" to whatever port you want the TigerVNC server to listen to.


## Usage
`runvncserver start|stop|restart|status`  

`start` - will start the TigerVNC Server on display :0 (scraping) default on port 5900  
`stop` - will kill the TigerVNC Server on display :0  
`restart` - will restart the TigerVNC Server on display :0 (if it's not running, it will just start it)  
`status` - will tell whether the TigerVNC Server is running or not

## Files
* *~/.vnc*  
main TigerVNC server user directory (if it doesn't exist, create it with `mkdir -p ~/.vnc`)
* *~/.vnc/passwd*  
password file for VNC Server (if it doesn't exist, create it with `vncpasswd`)
* *~/.vnc/logfile*  
logfile location (created by script)
* *~/.vnc/hostname:0.pid*  
pid file (created by script)

## Notes

### Kill the TigerVNC Server on command line
There's a command for killing the vnc server on the command line, by `vncserver -kill :0` if the vnc server runs at the :0 display.  
However, this command looks for the pid file in your *~/.vnc* directory.  
The pid file format must be as following: *~/.vnc/${HOSTNAME}${DISPLAY}.pid*  

### Automatic Start
If you want to automatically start with the Xsession, you can put it to your ~/.xsessionrc
Like this:

> user@linux:~$ cat ~/.xsessionrc  
> /home/user/runvncserver/runvncserver >/dev/null 2>&1

## TODO
In the future, I try to implement a separate logfile for the script, since the logfile stored in ~/.vnc/logfile has only the TigerVNC Server output.

## Author
István Sebestyén-Teleki

Any patches or suggestions are welcome!
