# EC-2 Console Instance Connection and Running Stardog From Local Machine

## EC-2 Console Setup And Copying Public Key To EC-2 Console
In your AWS console homepage, search for Instances. Click Instances on the Search Menu. After this action, go to the Instances dropdown on the left of the page and click Instances again. This will show you your currently running instances. 

![InstancesProcess](https://user-images.githubusercontent.com/109543462/217055106-5a380ed8-8713-47f0-bd2e-ceae9eceb365.PNG)
![InstanceProctwo](https://user-images.githubusercontent.com/109543462/217055157-0a0fa366-b62f-473a-9e65-73fd18dd2796.PNG)

Click on Instance-ID and click connect, then click connect again, which will take you to your EC-2 Console. 

On your EC-2 Console, type in this command 
> cat ~/.ssh/authorized_keys

This will showcase any SSH public keys you have in this file. Now, go to your local Unubuntu terminal to access your public key in the ~/.ssh directory. Your public key is the file that ends with .pub. 

Copy this public key and utilize this next command to paste your public key in to the EC-2 Console
> vi authorized_keys <br />
> type the letter i (to insert into the file) <br />
> Paste your copied public key <br />
> :wq to save and exit the file 

Your EC-2 is now updated with your public key. 

## Set up EC-2 Console to Private Key

The next step is to connect to AWS on your local machine. Type in these following commands 
> echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf > /dev/null (Conditional in the case of your local machine not being able to connect) <br />
> pwd <br />
> ls -lh /home/username/.ssh/privatekey(the file without the .pub extension) - Helps ensure that your filepath exists <br />
> ssh -i "/home/username/.ssh/privatekey" ubuntu@ec2-52-91-172-141.compute-1.amazonaws.com

Your local machine is now connected to the AWS EC-2 console and it should look something like the image below. Congratulations

![AWSSetup](https://user-images.githubusercontent.com/109543462/217062370-73cff9cd-5514-4ae4-85ba-3627c509188d.PNG)
