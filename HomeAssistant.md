# Install HA on top of Raspberry Pi OS

## Install

https://siytek.com/install-home-assistant-on-raspbian/

```
sudo apt-get install python3 python3-dev python3-venv python3-pip libffi-dev libssl-dev 

sudo apt-get install libopenjp2-7 libtiff-dev

sudo useradd -rm homeassistant -G dialout,gpio,i2c
sudo mkdir /srv/homeassistant
sudo chown homeassistant:homeassistant /srv/homeassistant
sudo -u homeassistant -H -s
python3 -m venv /srv/homeassistant
source /srv/homeassistant/bin/activate

python3 -m pip install wheel
pip3 install homeassistant

python3 -m pip install  hass-nabucasa==0.39.0
python3 -m pip install home-assistant-frontend==20201229.1

hass
```

## Check install

http://homeassistant.local:8123

or

http://homeassistant:8123

or

http://pi-ip-address:8123


## Setup auto start

```
sudo nano -w /etc/systemd/system/home-assistant@homeassistant.service

[Unit] 
Description=Home Assistant 
After=network-online.target 

[Service] 
Type=simple 
User=%i 
ExecStart=/srv/homeassistant/bin/hass -c "/home/%i/.homeassistant" 

[Install] 
WantedBy=multi-user.target

sudo systemctl --system daemon-reload

sudo systemctl enable home-assistant@homeassistant
```

## Camera

configuration.yaml

```
rpi_camera:

homeassistant:
  whitelist_external_dirs:
  - "/tmp"

camera:
  - platform: rpi_camera
    timelapse: 1000
    file_path: "/tmp/image.jpg"

```


