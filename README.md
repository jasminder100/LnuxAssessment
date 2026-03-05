# LnuxAssessment
# 1) Configure smtp in localhost.
sudo apt update
sudo apt install postfix mailutils -y

# Create a user in your localhost, which should not be able to execute the sudo command.

sudo useradd -m limiteduser
sudo passwd limiteduser
groups limiteduser
sudo deluser limiteduser sudo
groups limiteduser


# 3) Configure your system in such a way that when a user type and executes a describe command from anywhere of the system it must list all the files and folders of the user's current directory.
Ex:- $ describe
$ content1 content2
Content3 content 4

sudo nano /usr/local/bin/describe
cat /usr/local/bin/describe
ls -ld /usr/local/bin/describe
sudo chmod +x /usr/local/bin/describe
describe
cd /
describe
cd /etc
describe
cd /tmp
describe

# 3) Create a service with the name showtime , after starting the service, every minute it should print the current time in a file in the user home directory.

sudo vi /etc/systemd/system/showtime.service

[Unit]
Description = Show current time in user home directory

[Service]
ExecStart =  /bin/bash -c 'while true; do date >> /home/sigmoid/showtime.log; sleep 60; done'
Restart = always

[Install]
WantedBy = multi-user.target

sudo systemctl daemon-reload
sudo systemctl enable showtime
sudo systemctl start showtime
sudo service showtime status
sudo systemctl stop showtime
cat /home/sigmoid/showtime.log

# 4) i) Users can put a compressed file at any path of the linux file system. The name of the file will be research and the extension will be of compression type, example for gzip type extension will be .gz. You have to find the file and check the compression type and uncompress it.

# ii) Configure your system in such a way that any user of your system creates a file then there should not be permission to do any activity in that file

i) touch research
echo "This is sample data" > research
gzip research
ls
sudo mv research.gz /tmp/
sudo find / -type f -name "research.*" 2>/dev/null
file /tmp/research.gz
gunzip /tmp/research.gz

ii) umask 666
touch newfile
ls -l newfile
exec bash
sudo nano /etc/profile - write umask 666
output - ---------- 1 root root 0 Mar  5 00:29 newfile
