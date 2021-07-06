# net scan web application



This simple net scanner web app lets you scan any network you are connected to by slightly tweaking the gateway IP address and the corresponding subnet mask. All I used was the following


## Features

- Lets you scan any network you are connected to 
- You can basically set the refresh time for the cronjob to run
- Runs on your laptop, desktop or your phone! 
- Lists the IP addresses, MAC addresses and any open ports for the connected devices
- A very useful tool for any IT nerd


## Tech

Dillinger uses a number of open source projects to work properly:

- Ubuntu running machine
- PHP -  Very little scripting
- nmap 
- Apache Server
- ✨Cronjobs ✨``` yes that is fancy ```



## Set Up

Fairly simple steps in starting this up

1. On your Linux machine, you need to, if not already, set up Apache server, nmap and php

```sh
sudo apt-get install apache2
sudo apt-get install nmap
sudo apt-get install php
```

2. Once done, let's move on to fiddling with the local www files

```sh
cd ..
cd /var/www
```

3. Check for permissions on the ```html``` folder and ensure appropriate permissions are given. I went with 777. and FYI - ```html``` is the folder which contains the files that run the show


4. In the same directory we then execute the following: 
```sh
sudo crontab -e 
```
5. This is where things get a bit untidy - not soo much though. I referred to https://crontab.guru/, to help me with perfectly setting up the cronjob timings right. After running the above command, you are basically in a file editor, and by pressing the down key, you come all the way down and enter the following- 
```sh
*/10 * * * * nmap 10.0.0.1/24 -oN /var/www/html/nmap.html
```
6. This basically means that at every 10th minute of the day, nmap will scan the given ip address and output its results to the nmap.html file specified on that path. Gives you the proper gist, doesn't it?! 
7. Once done, press ctrl+x and then it asks if you want to save it, so Y and then enter. And you are back to your normal Terminal screen. 
8. Next comes the ```network.php```, which includes the script that displays the results in the web browser or your phone browser - 
```sh
<?php
echo "Server Timestamp: ";
echo date("h:i:sa");
echo "<pre>";
include("nmap.html");
echo "</pre>";
?>
```
9. Gorgeous, beautiful, elegant and does the job seriously well. Timestamp and Date should be obvious, the ```<pre>``` tag basically formats neatly the output of the ```nmap.html``` file. If you dry run the ```nmap.html``` file. you basically see a big chunk of data, and it is hard to interpret- similar to unmanaged ethernet cables hanging out of a server rack. Ugly isin't it! 
10. The last part, open your browser and type in the url localhost/network.php and you see all them devices listed, slowly sucking the bandwidth out of your internet. 


## Development

Want to contribute? Great!

I am looking for ideas to make the output page a bit more interactive and lively! Since this is something I did way back in my first year of school, I have not had a chance to work with it, but for sure it can be made into a more presentable piece. Let me know what you think! 


**Free Software, Hell Yeah!**


