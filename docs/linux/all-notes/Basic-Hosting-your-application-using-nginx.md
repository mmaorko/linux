If you want to host multiple application on a single IP then you must use different port lets try.
Since we may need to manage many application, best practice is to keep all application configurations within the site available 
`/etc/nginx/sites-available/` . 
There may be multiple project/site within the sites-available. but here you need to enable site link to activation to link up.  then need to should be soft link those application.
 
#### Step-1:
You need to go 
```
cd /etc/nginx/sites-available/
```
 and  check using `ll` then copy "default" which are located here and it's a configure file.
 
![enter image description here](https://i.ibb.co.com/M6QrmLP/2025-01-08-124419.png)

now copy this default file. best practice try to put your application name for easy to find out application.

```
sudo cp default domain.com
``` 
Then, Open confugure file

![enter image description here](https://i.ibb.co.com/R2T40Ts/2025-01-08-125233.png)

Firstly Need to change the port number. otherwise your site not working. Your port number should be 4 character and we know, well know port is 1 to 1024 and useable port 1023. when we configure a port must be remember your given port should be outside of this.
best practice to give your IP in your application configuration file 

![enter image description here](https://i.ibb.co.com/Mpv6SM8/new.jpg)
#### Step-2:
Then you need to active this configure file. If you want to activate, you have to link up it to the site enable.
``` 
sudo ln -s /etc/nginx/sites-available/domain.com /etc/nginx/sites-enabled/
```
Then check your applicatioin active successfully ok or not
```
ls -la /etc/nginx/sites-enabled/
```
 
Then check nginx all configuration using

`sudo nginx -t`
when everything is ok then reload or restart your nginx
```
sudo nginx -s reload
or
sudo systemctl restart nginx
```
now check your site/application using port number like this 192.168.1.28:8080
