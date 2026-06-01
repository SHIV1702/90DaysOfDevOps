############################   Linux Commands Cheatsheet   ######################################

1. Commands Used in Process management -

<<<<<<< HEAD
Command                   :Purpose

ps -ef                    :list all running process 
   
ps -aux                   :show detailed process information

top                       :Real-time process monitoring                   

htop                      :interactive process veiwer

kill -9 PID               :Forcefully kill any process 

pkill -U username         :kill all processes running by specific user

free -h                   :check memory usage 

uptime                    :shows system run time since last reboot, system load, no. of user logged in 

sar                       :Historical performance statistics

#####################################################################################################

2. File System Commands

Command                   :Purpose

pwd                       :Show current directory

ls                        :list file & directories 

ls -l                     :detailed listing 

ls -la                    :list hidden files also

cd                        :change directory

touch                     :create empty file

mkdir                     :make directory

cp                        :copy file

cp -r                     :copy directory

mv                        :rename file or directory 

rm                        :delete file 

rm -r                     :delete directory

cat                       :to view file content

df -h                     :show disk space usage

du -sh                    :show specific directory size

chmod                     :change permission of file 

chown                     :change owner of file

chgrp                     :change group of file 

ln                        :to make hard link 

ln -s                     :to make soft link

#############################################################################################

3. Networking Commands 

Command                   :Purpose 

nslookup google.com       :DNS lookup 

dig google.com            :Detailed DNS query

cat /etc/resolv.conf      :DNS server configuration file 

netstat -anu              :display network connections and statistics.

curl https://google.com   :Test Web connectivity

wget URL                  :Download file from URL 
