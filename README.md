# RTC DS 1302 on Raspberry Pi 3 Model B under CentOS 7

## Compiling and Installing

To compile and install RTC DS 1302 module, run commands below.

```

yum group install -y "Development Tools"

cd /var

mkdir development

cd /var/development

rm -rf rtc-pi.c

curl --location https://github.com/kamshory/RTCRaspberryPi3BCentOS7/blob/master/rtc-pi.c > rtc-pi.c

cd /var/development

cc rtc-pi.c -o rtc-pi 

rm -rf /usr/sbin/rtc-pi

cp rtc-pi /usr/sbin/

echo -e '[Unit]' > /usr/lib/systemd/system/rtc.service

echo -e 'Description=rtc' >> /usr/lib/systemd/system/rtc.service

echo -e '' >> /usr/lib/systemd/system/rtc.service

echo -e '[Service]' >> /usr/lib/systemd/system/rtc.service

echo -e 'ExecStart=/usr/sbin/rtc-pi' >> /usr/lib/systemd/system/rtc.service

echo -e '' >> /usr/lib/systemd/system/rtc.service

echo -e '[Install]' >> /usr/lib/systemd/system/rtc.service

echo -e 'WantedBy=multi-user.target' >> /usr/lib/systemd/system/rtc.service

/usr/sbin/rtc-pi `date +"%Y%m%d%H%M%S"`

systemctl start rtc.service

systemctl enable rtc.service

reboot

```
