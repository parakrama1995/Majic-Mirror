#Auto Starting MagicMirror
The methods below describe ways to automatically start you MagicMirror on boot, and even ways to keep it running in case of a failure. 

##Using PM2
PM2 is a production process manager for Node.js applications with a built-in load balancer. It allows you to keep applications alive forever, to reload them without downtime and to facilitate common system admin tasks. In this case we will use it to keep a shell script running.

###Install PM2
Install PM2 using NPM:
````
sudo npm install -g pm2
````

###Starting PM2 on Boot
To make sure PM2 can do it's job when (re)booting your operating system, it needs to be started on boot. Luckily, PM2 has a handy helper for this. 
````
pm2 startup
````
PM2 will now show you a command you need to execute.

###Make a MagicMirror start script.
To use PM2 in combination with MagicMirror, we need to make a simple shell script. Preferable, we put this script outside the MagicMirror folder to make sure it won't give us any issues if we want to upgrade the mirror.
````
cd ~
nano mm.sh
````
Add the following lines:
````
cd ~/MagicMirror
DISPLAY=:0 npm start
````
Save and close, using the commands `CTRL-O` and `CTRL-X`.
Now make sure the shell script is executable bij performing the following command:
````
chmod +x mm.sh
````
You are now ready to the MagicMirror using this script using PM2.

###Starting your MagicMirror with PM2
Simply start your mirror with the following command:
````
pm2 start mm.sh
````
You mirror should now boot up and appear on your screen after a few seconds.

###Enable restarting of the MagicMirror script.
To make sure the MagicMirror restarts after rebooting, you need to save the current state of all scripts running via PM2. To do this, execute the following command
````
pm2 save
````

And that's all there is! You MagicMirror should now reboot after start, and restart after any failure.

###Controlling you MagicMirror via PM2.
With your MagicMirror running via PM2, you have some handy tools at hand:
#### Restarting your MagicMirror
````
pm2 restart mm
````
#### Stopping your MagicMirror
````
pm2 stop mm
````
#### Show the MagicMirror logs
````
pm2 logs mm
````
#### Show the MagicMirror process information
````
pm2 show mm
````
