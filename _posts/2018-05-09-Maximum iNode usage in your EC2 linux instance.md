One of the EC2 linux servers running Ubuntu 16.04 i maintain had space issues.
When i ran df -h , it showed the root partition had still got 2.6gb free space left and yet the server kept throwing disk space issues.

Running df -i showed the root cause of the problem , which was maximum iNodes usage which was at 100 % for the root partition.

Steps to bring down the iNodes usage

Find out which is consuming maximum number of iNodes

Log in as root user in your EC2 instance- sudo su

Run as root user:
for i in /*; do echo $i; find $i |wc -l; done

In my case the /usr had the highest number-  /usr 485722

Digging deeper in the /usr directory

for i in /usr/*; do echo $i; find $i |wc -l; done

/usr/bin
762
/usr/games
1
/usr/include
20
/usr/lib
7818
/usr/local
29
/usr/sbin
185
/usr/share
23009
/usr/src
453897


Further digging into /usr/src

for i in /usr/src/*; do echo $i; find $i |wc -l; done

/usr/src/linux-headers-4.4.0-64
16899
/usr/src/linux-headers-4.4.0-64-generic
9786
/usr/src/linux-headers-4.4.0-70
16899
/usr/src/linux-headers-4.4.0-70-generic
9788
/usr/src/linux-headers-4.4.0-71
16899
/usr/src/linux-headers-4.4.0-71-generic
9788
/usr/src/linux-headers-4.4.0-72
16899
/usr/src/linux-headers-4.4.0-72-generic
9788
/usr/src/linux-headers-4.4.0-75
16898
/usr/src/linux-headers-4.4.0-75-generic
9787
/usr/src/linux-headers-4.4.0-78
16898
/usr/src/linux-headers-4.4.0-78-generic
9792
/usr/src/linux-headers-4.4.0-79
16898
/usr/src/linux-headers-4.4.0-79-generic
9792
/usr/src/linux-headers-4.4.0-81
16898
/usr/src/linux-headers-4.4.0-81-generic
9792
/usr/src/linux-headers-4.4.0-83
16898
/usr/src/linux-headers-4.4.0-83-generic
9792
/usr/src/linux-headers-4.4.0-87
16899
/usr/src/linux-headers-4.4.0-87-generic
9792
/usr/src/linux-headers-4.4.0-89
16900
/usr/src/linux-headers-4.4.0-89-generic
9792
/usr/src/linux-headers-4.4.0-91
16900
/usr/src/linux-headers-4.4.0-91-generic
9792
/usr/src/linux-headers-4.4.0-92
16900
/usr/src/linux-headers-4.4.0-92-generic
9792
/usr/src/linux-headers-4.4.0-93
16900
/usr/src/linux-headers-4.4.0-93-generic
9792
/usr/src/linux-headers-4.4.0-96
16941
/usr/src/linux-headers-4.4.0-96-generic
9804
/usr/src/linux-headers-4.4.0-97
16941
/usr/src/linux-headers-4.4.0-97-generic
9804
/usr/src/linux-headers-4.4.0-98
16952
/usr/src/linux-headers-4.4.0-98-generic
9804

So it's the kernels taking up too much iNodes usage. I had to remove few kernels manually as i was not able to run the apt-get commands in the following manner

sudo rm -rf /usr/src/linux-headers-4.4.0-70/*

sudo rm -rf /usr/src/linux-headers-4.4.0-70-generic/*

Use uname -mrs to check the kernel currently being used so that you don't delete it accidentally.
As i removed enough kernels manually i could free up some iNodes , which finally let me run the sudo apt-get autoremove -f .
Now the iNodes usage was brought down from to 68% from 100% .


