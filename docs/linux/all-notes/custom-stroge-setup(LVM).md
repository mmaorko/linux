# Configure custom storage setup Linux Ubuntu server (LVM)

***LVM*** 
LVM (Logical Volume Manager) is a flexible and powerful disk management system in Linux that allows administrators to manage disk space more efficiently. it redefines how Linux manages storage and You can create logical volumes of any size and shape, and adjust them as your needs change

**LVM Setup Storage Management step by step**

 1. First of all select the custom storage layout then click done.
    
 ![enter image description here](https://i.ibb.co.com/LR3mfMw/1.png)
 
 2. Select free space, and create a volume for boot![enter image description here](https://i.ibb.co.com/dLjqQMw/2.png)

 ![For boot space Volume](https://i.ibb.co.com/3Yx3sFg/3.png)
 

 3. Then again click the free space and GPT partition to /dev/sda ![enter image description here](https://i.ibb.co.com/vXnX9ZD/5.png)
 
 4. Then create an LVM volume group for Creating single logical volumes of multiple physical volumes or entire hard disks 
    ![LVM volume group](https://i.ibb.co.com/Y8vJpmK/6.png)

 6. Then again click the free space and add logical volume under home ![enter image description here](https://i.ibb.co.com/hXvHNqV/7-logical-volume-create.png)

 7. Add logical volume for the database server ![enter image description here](https://i.ibb.co.com/sqNJ1M5/7-logical-volume-create-for-database-inside-var.png)

