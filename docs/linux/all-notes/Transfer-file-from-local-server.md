#### step-1:  File Transfer 
open file which folder located on your file, then open the terminal , then first of all tar the file 
```
tar -cvf world-cup.tar world-cup

--default port--
sudo scp file.tar server@192.168.1.28/:/home/server
--For Custom Port--
sudo scp -P 8888 file.tar server@192.168.1.1:/home/server
```
#### Step-2: Connect server
then type `ll` and enter to see the all file list 
```
ll
```
extract the tar file using 
``tar xvf world-cup.tar``
then again check the file using `ll`
#### Step-3: name minimize/short if need and move file to var/www
``mv world-cup worldcup``
then again check to see it's done or not

move file var/www
mv-use to move file
``sudo mv worldcup/ /var/www/``
-then check var/www file using `cd /var/www/` and check using `ll`
-then open the file using``/var/www/worldcup/`  
![enter image description here](https://i.ibb.co.com/fr86TfY/Whats-App-Image-2025-01-05-at-16-17-23-39188abb.jpg)
```
sudo vim /etc/ngnix/sites-available/default
```
them configure `roo /var/www/put yout site name here ` then reload nginx and check
![enter image description here](https://i.ibb.co.com/LR3LgC7/Whats-App-Image-2025-01-05-at-16-24-06-7dd828cf.jpg)


then reload nginx and check
