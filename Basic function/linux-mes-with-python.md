`Python script to send Telegram notifications based on the log file` <br>
Dự án này cho phép bạn ghi lại các sự kiện giao dịch trong MT4 và sử dụng tập lệnh Python để gửi thông báo Telegram dựa trên tệp nhật ký.<br>
Đây là hướng dẫn dùng script python để lấy nhật ký của mt4 và gửi đến telegram.<br>
Cách làm này giúp giảm tải cho MT4, giúp EA chạy mượt hơn.<br>

This project allows you to log trading events in MT4 and use a Python script to send Telegram notifications based on the log file.<br>
This method helps reduce the load on MT4 by offloading message sending to Python. <br>


```bash
# Kiểm tra phiên bản Python: Mở terminal và chạy lệnh sau để kiểm tra phiên bản Python đã cài đặt
# Check Python version: Open terminal and run the following command to check the installed Python version
python3 --version

# Nếu Python chưa được cài đặt hoặc phiên bản quá cũ, bạn có thể cài đặt Python 3 bằng lệnh sau
# If Python is not installed or the version is too old, you can install Python 3 with the following command
sudo apt update && sudo apt install python3 python3-pip -y

# Cài đặt thư viện requests - Install requests library
pip3 install requests

```

```bash
#MT4: Log Trading Events
#Use FileOpen() in MT4 to log trade events (such as opening or closing orders) to a file (e.g., trade_log.txt).

void WriteLog(string message)
{
    int fileHandle = FileOpen("trade_log.txt", FILE_CSV|FILE_WRITE|FILE_READ|FILE_APPEND);
    if(fileHandle != INVALID_HANDLE)
    {
        FileWrite(fileHandle, TimeToString(TimeCurrent(), TIME_DATE|TIME_MINUTES), message);
        FileClose(fileHandle);
    }
}

```

```bash
# Python Script: Read Log and Send Telegram Messages
# The Python script reads the MT4 log file every 10 seconds and sends the latest entries as Telegram messages.


# Tạo file Python - Create Python files
nano mt4_telegram_bot.py


import time
import requests

bot_token = 'your-telegram-bot-token'
chat_id = 'your-chat-id'

def send_telegram_message(message):
    url = f"https://api.telegram.org/bot{bot_token}/sendMessage"
    payload = {'chat_id': chat_id, 'text': message}
    requests.post(url, data=payload)

def check_log_and_send():
    with open('/path/to/mt4/log/trade_log.txt', 'r') as f:
        lines = f.readlines()
    for line in lines[-5:]:
        send_telegram_message(line.strip())

while True:
    check_log_and_send()
    time.sleep(10)

```

```bash
# Run Python Script - Ensure Python is installed, and install requests library:
pip3 install requests

# Run the script
python3 mt4_telegram_bot.py


# Optional: Run Python Script in the Background
# Use nohup or screen to keep the script running in the background
nohup python3 mt4_telegram_bot.py &

```

nếu chưa cài đặt ubuntu deskop, tìm hướng dẫn ở linux-metatrader. <br>
If you haven't installed Ubuntu desktop yet, find guid on linux-metatrader

Any problem :  https://t.me/MwForexTrading

`>>>From NamHenry`


