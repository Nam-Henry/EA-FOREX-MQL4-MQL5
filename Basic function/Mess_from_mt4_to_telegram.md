```bash

void SendTelegramMessage(string message)
{
   string botToken = "XXXXXXXXXXXXXXXXXXXXXXXXXX";  // Thay bằng token của bot - Replace with the bot's token
   string chatID = "XXXXXXXXXXXX";      // Thay bằng chat ID - Replace with chat ID 
   string url = "https://api.telegram.org/bot" + botToken + "/sendMessage";
   
   string postData = "chat_id=" + chatID + "&text=" + message;
   char postDataArray[];
   StringToCharArray(postData, postDataArray);
   
   char result[];
   string headers;
   int timeout = 5000; // Timeout 5s

   int res = WebRequest(
      "POST",                       
      url,                         
      headers,                      
      timeout,                     
      postDataArray,                
      result,                       
      headers                      
   );
   
   if(res == -1)
   {
      Print("Err WebRequest: ", GetLastError());
   }
   else
   {
      Print("Telegram notification sent successfully: ", message);
   }
}

```

Lưu ý:
WebRequest() cần quyền truy cập internet từ MetaTrader 4. <br>
Bạn cần thêm địa chỉ URL `https://api.telegram.org` <br>
vào phần Tools → Options → Expert Advisors trong MetaTrader để cho phép EA thực hiện kết nối.<br>
Chat ID và Bot Token cần phải thay đúng để gửi thông báo đến đúng bot và chat của bạn.

Note:
WebRequest() requires internet access from MetaTrader 4.<br>
You need to add the URL `https://api.telegram.org` <br>
Go to Tools → Options → Expert Advisors in MetaTrader to allow the EA to make the connection.<br>
Chat ID and Bot Token need to be changed correctly to send notifications to the correct bot and your chat.<br>

Get more: https://t.me/MwForexTrading

```bash
void OpenBuyOrder()
{
   int ticket = OrderSend(Symbol(), OP_BUY, 0.1, Ask, 3, 0, 0, "Buy order", 0, 0, Green);
   if(ticket > 0)
   {
      SendTelegramMessage("EA has opened a Buy order: " + Symbol());
   }
}

void CloseOrder(int ticket)
{
   if(OrderClose(ticket, OrderLots(), Bid, 3, Red))
   {
      SendTelegramMessage("EA closed orders: " + Symbol());
   }
}

```
