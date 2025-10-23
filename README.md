[![](https://github.com/TechTutoPPT/Notion2API/blob/main/IMG_8420.PNG)](https://youtu.be/6pHoXXdjrC4)

notion-2api這項目是將Notion AI轉換為兼容OpenAI的API, 
```
https://github.com/lzA6/notion-2api
```
這項目可部署到Docker上, 再透過Chatbox引用API方式便能使用GPT5及Sonnet4.5

以下是部署過程:
開啟已安裝Docker的WSL Ubuntu終端, 
更新套件庫:
```
sudo apt update 
```
安裝git:
```
sudo apt install git
```
克隆notion-2api項目:
```
git clone https://github.com/lzA6/notion-2api.git
```
移動至notion-2api資料夾:
```
cd notion-2api
```
將配置文件範本複製成配置文件:
```
cp .env.example .env
```

以Edge瀏覽器登入或註冊Notion:
```
https://www.notion.com/
```
於Notion主版面按F12以開啟開發者工具, 點選"應用程式"選頁, 展開Cookies, 點選https://www.notion.so, 於名稱點選token_v2將其值複製下來.
切換到"網路"選頁, 點選名稱以get作開頭的項目,  拖拉卷軸至最下方查找X-Notion-Active-User-Header及X-Notion-Space-Id, 將其值複製下來.
點Notion左上角的帳戶資料, 將名稱及電郵複製下來.

返回WSL Ubuntu終端, 編輯配置檔:
```
sudo nano .env
```

將記下的資訊填入相關位置:
API_MASTER_KEY="你API的密碼"
NGINX_PORT="你設立的端口"
NOTION_COOKIE="你token_v2的值"
NOTION_SPACE_ID="你X-Notion-Space-Id的值"
NOTION_USER_ID="你X-Notion-Active-User-Header的值"
NOTION_USER_NAME="你Notion的名字"
NOTION_USER_EMAIL="你Notion的電郵地址"

啟動notion-2api:
```
docker-compose up -d --build
```

下載Chatbox:
```
https://github.com/chatboxai/chatbox/releases
```
執行Chatbox-1.15.4-Setup.exe安裝應用, 安裝後開啟Chatbox進入主版面, 點左下方設定>模型提供方>OpenAI>
API金鑰填上"你API的密碼"
API主機填上http://localhost:8088/v1/chat/completions
再按檢查, 如果顯示連接成功!便可點選下方的獲, 減選所有預設模型, 加選claude-sonnet-4.5, claude-opus-4.1, gpt-4.1, gpt-5
完成後點選新對話, 選用剛才的模型向它發問便可.
