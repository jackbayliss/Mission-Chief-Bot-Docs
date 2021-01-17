# Welcome to MissionChief Bot

## Getting the bot
1. All users must sign up via the [website](https://missionchiefbot.com/)
2. Pay, Payment is taken monthly, but the pricing is simple- it's £1 p/m per account and all done via the website above.
3. Once you've paid you'll see new options on the dashboard, simply click "add-user" and add your ***in game name*** there.
4. Download the newest release via GitHub for your operating system.
5. Extract the bot and edit the config to add your login information
6. Run the generator! (generate.exe/.py) The generator is required in order to create mission files, without those the bot simply won't operate.
7. Run the bot!

## Main Files

### Main bot files
1. MissionChiefBot - This is the main bot, this will run the despatching tasks etc.
2. Restarter - This effectively is a cradle for the MissionChiefBot- if it major crashes (i.e exits) at all the bot will be auto restart. Usually good for people that want to run it while they're asleep etc.
3. generate - This is in charge of grabbing new missions and the data, make sure you manually run this every time there's new missions.

### Config file
The config file is found in the config.ini, any editiable options for the user will always be in there.

### File structure
The bot follows a simple folder structure. The main files will always be in the main directory. Anything to do with the bot in terms of operations or missions will be found in the `json` folder.
#### Missions
Missions are found in the json folder, then into regions, then in your selected region, then into the missions folder. These missions are completely customizeable by the user. The bot will follow any edited missions.

#### Links / Missing.json
These files essentially tell the bot which category belongs to which vehicles. Because the game can vary in names (i.e plural non-plural) these files can be edited and changed. 

## Running via AWS
### Initial Setup
1. Sign up for AWS via [here](https://portal.aws.amazon.com/billing/signup?refid=jackbaylissgithub)
2. Ensure you enter your card details etc, and verify your account (dont worry, you wont be charged for the server we will be using the free tier- your card may be charged $1 to verify your card)
3. Once you're in go to your console via [this](https://console.aws.amazon.com) link
4. In the find services search, type in `EC2` and click it- or if you don't have this click `Launch a virtual machine` it'll do the same thing.
5. Check on the top right that your region is correct for where you live- I.E UK would be London etc.
6. In the top search type in `Docker` and click enter. You should see something similar to `Amazon Linux AMI 2018.03.0 (HVM` ensure that it says `FREE TIER ELIGIBLE` at the bottom. This will make sure it's free. 
7. Click select on the right hand side.
8. Click the `free tier eligible` instance, for me it's `t2.micro` ensure it's selected and click `Review and launch instance`
9. Click launch
10. Click `create a key pair` - enter a random name and download the file **KEEP THIS FILE SAFE**
11. Click `view instances`
12. Wait around 4 minutes for the instance to get started.

### Connecting to your EC2 instance
1. Assuming you're still on the instance page, click the instance you just made and click `connect` at the top
2. The easiest thing to do is click `EC2 Instance Connect (browser-based SSH connection)` this will connect you to the server via the browser-- or the alternative it to use PuTTY (If you don't want to use PuTTY skip to number 10) continue below on how to use PuTTY 
3. So, you want to use PuTTY, first thing first download PuTTY- and install it.
4. Once installed open PuTTYgen, and click `load` then select your .pem key you saved earlier. Make sure you change the file type to `all`
5. Click `save private key` and save it to somewhere you know... 
6. Now open PuTTY, on the left hand side go to connection -> ssh and then auth.
7. Under private key file click browse, and select the file you just made.
8. Now, finally we can go back to Amazon, click connect again and this time click `a standalone SSH client` you'll see a name similar to `ec-23-23232332.compute.amazonaws.com`copy this name go back to Putty and go to Session on the left hand side at the top. Paste the name into there and then-- click connect.
9. Your black box will say `login as:` just type in `ec2-user` and click enter.
10. You're in!
11. Type `sudo yum update -y` and click enter, then do `sudo yum install docker -y`
12. Type `sudo service docker start` and let it complete. Then do `sudo usermod -a -G docker ec2-user`

### Bot installation
1. Once you're in type in `sudo docker pull jjbayliss/mission-chief-v2`, let it run it'll set up the image for the bot. 
 
2. Once the image is done simply run `sudo docker run -it -d jjbayliss/mission-chief-v2`. This will create a container for you.

3. Run `sudo docker ps -a` and copy the name of your container there should only be one, then run `sudo docker exec -it [container name] bash` this will take you into the container in a bash.
4. You should be brought straight into a container, all you'll need to do is `cd Mission-Chief-Bot`


5. type `git checkout -f` followed by `git pull origin mac` this will update the bot to the newest version. 




6. Next do `vim config.ini` you'll want to press the `I` key to edit the document, and add your username, password and region etc. Once done press `ESC` and type `:wq` this will save the document.

7. Run `python3.9 MissionChiefBot.py` to run the base bot, and you're done!
8. To exit the docker container press `CTRL + D`, and if you need to enter the bot again just follow from step 6.

## Running the bot on Digital Ocean
### Sign Up
1. First of all I'd recommened setting up a Digital Ocean account, or any other cloud provider that you can use Docker with. You can set an account for Digital Ocean [here](https://m.do.co/c/741cf5923606) (It's a referral link)

(Make sure you install docker if you're going outside of DO)

2. Once you've signed up to Digital Ocean simply create a droplet. You can install docker straight to it via the marketplace so i'd suggest doing that. (You can use any droplet, this will work on the smallest $5 A month one)

### Installing the bot to the droplet
3. Connect into the droplet, you can do this via going to the Access Console or alternatively SSH into the droplet.

4. Once you're in type in `docker pull jjbayliss/mission-chief-v2`, let it run it'll set up the image for the bot. 
 
5. Once the image is done simply run `docker run -it -d jjbayliss/mission-chief-v2`. This will create a container for you.

6. Run `docker ps -a` and copy the name of your container there should only be one, then run `docker exec -it [container name] bash` this will take you into the container in a bash.

7. You should be brought straight into a container, all you'll need to do is `cd Mission-Chief-Bot`


8. type `git checkout -f` followed by `git pull origin mac` this will update the bot to the newest version. 


9. Next do `vim config.ini` you'll want to press the `I` key to edit the document, and add your username, password and region etc. Once done press `ESC` and type `:wq` this will save the document.

10. Run `python3.9 MissionChiefBot.py` to run the base bot, and you're done! (bare in mind you'll need to run git pull to update the repo)

11. To exit the docker container press `CTRL + D`, and if you need to enter the bot again just follow from step 6.