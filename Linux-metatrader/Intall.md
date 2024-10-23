`gui ubuntu and rdp`
Here are guid for installing ubuntu desktop and metatrader

```bash

#+------> installing ubuntu desktop - cài đặt ubuntu desktop

#update ubuntu - Cập nhật hệ thống
sudo apt update && sudo apt upgrade -y

#install xubuntu-desktop - cài đặt xubuntu
sudo apt install xubuntu-desktop

#then choice light dm - sau quá trình chạy xong chọn light dm
sudo dpkg-reconfigure lightdm

#install xrdp - cài đặt X Remote Desktop Protocol
sudo apt install xrdp
sudo systemctl status xrdp

#add new user
sudo adduser xrdp ssl-cert
sudo systemctl restart xrdp

#open port ufw (optional if you use ufw) - nếu bạn dùng tưởng lửa thì mở cổng 3389.
sudo ufw allow 3389

#config rdp 
sudo service xrdp stop

#//+------->
nano /etc/xrdp/startwm.sh
# Comment the last 2 lines - comment 2 dòng cuối bằng việc thêm # trước dòng code.
# add this line at the end - sau đó thêm dòng này vào bên dưới
startxfce4

sudo systemctl restart xrdp

#=> Remote Desktop to see the results. - mở Remote Desktop và thụ hưởng thành quả lao động.
NOTE: USER and PASS is the information you register for vps

### add this option if there is an error - thêm bước này để bớt lỗi.

sudo apt remove gnome-terminal
sudo apt install gnome-terminal
```
```bash
#+------> installing metatrader - cài đặt mt4 hoặc mt5.

# MT4
wget https://download.mql5.com/cdn/web/metaquotes.software.corp/mt4/mt4ubuntu.sh ; chmod +x mt4ubuntu.sh ; ./mt4ubuntu.sh

#source/ Nguồn =>> https://www.metatrader4.com/en/trading-platform/help/userguide/install_linux

# MT5
wget https://download.mql5.com/cdn/web/metaquotes.software.corp/mt5/mt5ubuntu.sh ; chmod +x mt5ubuntu.sh ; ./mt5ubuntu.sh

#source/ Nguồn =>> https://www.mql5.com/en/articles/625
```


Bởi dùng VPS nên bạn có thể biết trực tiếp EA trên vps để chạy hoặc có thể tải lên file EA bằng SFTP
Khuyến nghị sử dụng TERMIUS

Because you use VPS, you can directly know the EA on the vps to run or you can upload the EA file using SFTP.
Recommended use of TERMIUS

Any problem :  https://t.me/MwForexTrading

`>>>From NamHenry`
