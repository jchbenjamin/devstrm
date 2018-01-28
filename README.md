# devstrm
device stream

#General installation instructions
Required items
* working Linux workstation
* flash drive pref 8GB
* ssh compatible embedded system intending to install Linux flavor (raspi?)


#Components Overview

	Client

		Use react-native to build viewer for race na

			Nodejs: base software

			React-Native

	Server

	Raspbian Lite on a Raspberry Pi Zero W or 3

		Web server component

			Nginx Environment

		Disc Extraction Component

			ivman script that on new disc:

				checks for disc:

					if none:

						make sure server clean

					if new:

						runs VLC to extract DVD content to mp4


			script to build JSON output to client

		


#TECH STACK

	React-Native - Client

	Nginx - Server

	PHP5 - Web auth

	HTML5 - Internet Streaming

	libdvdcss/Handbrake - Video Codecs

	Raspbian/ Linux - Operating System

	Raspberry Pi - Hardware

	

#RASPI SERVER SETUP

directions for setting up raspberry pi from

fresh raspbian lite image

On Workstation:
sudo dd bs=4M if=raspstretch.img of=/dev/sdb status=progress conf=fsync
(/dev/sdb should be the flash drive inserted in workstation)
(raspstretch.img is up to date image from internet)

#Create f2fs video partition
sudo gparted
Modify root fs so that there is empty space after it
If gparted does not allow operation, incrementally modify by 1GB

sudo apt-get install f2fs-tools
sudo mkfs.f2fs -l videofs /dev/sdb3



Use credentials user:pi pass:raspberry to login to installed system

sudo raspi-config

CHANGE ROOT PASSWORD
Set up SSH credentials for home wireless
Localization: EN US UTF-8
Change keyboard localization
change timezone

Exit and save

sudo ifconfig
Find ip address to wlan0 interface

restart system
Unplug monitor and log in from ssh terminal
ssh pi@{ipaddress}

go to /etc/apt/sources.list add line
deb http://reflection.oss.ou.edu/raspbian/raspbian/ stretch main contrib non-free rpi
comment all others out

#Add f2fs video partition to file partition table
sudo mkdir /mnt/vid

sudo blkid
copy information from blkid for videofs into /etc/fstab:
PARTUUID=7e3a6175-03  /mnt/vid  f2fs            defaults,noatime        0       1

#INSTALL NGINX

sudo apt-get install nginx

modify /etc/nginx/nginx.conf


#Device scripting
todo
scripts to enable ripping when dvd is inserted


#build react front-end

/var/www/html

build docker container for service



#Make Handbrake


go to /etc/apt/sources.list add line
deb http://reflection.oss.ou.edu/raspbian/raspbian/ stretch main contrib non-free rpi
comment all others out

sudo apt-get update

sudo apt-get install -y libmp3lame-dev libass-dev libsamplerate-dev libopus-dev libxml2-dev libvorbis-dev libjansson-dev libtool-bin libbz2-dev libx264-dev libtheora-dev libdvdread-dev libdvd-pkg libfontconfig1-dev libexpat1-dev libavcodec-dev libfreetype6-dev libsamplerate-dev cmake yasm build-essential

sudo dpkg-reconfigure libdvd-pkg

export PKG_CONFIG=/usr/bin/pkg-config && export PKG_CONFIG_PATH=/usr/lib/pkgconfig

./configure --disable-gtk --force --disable-x265 --disable-fdk-aac --enable-libav-aac
cd build
sudo make install

HandBrakeCLI -i /dev/sr0 -e x264 -f av_mp4 -T -r 23.976 -t 1 -c "1-2" -q 20 -B 80 --keep-display-aspect --display-width 320 -O -o /var/www/html/test.m4v



#end

cp Handbrake* ~

cd ~

tar xvjf Handbrake*

cd Handbrake*

./configure

cd build

make


script to run on disc detect:

use ivman



For Client:

Install Node.js latest


Install React Native

npm install -g create-react-native-app


Video React

npm install —save video-react react react-do redux

follow directions for React Native to use with Expo


Install handbrake



