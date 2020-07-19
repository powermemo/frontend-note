# SASS

## 安裝等前置作業

1. **安裝NODE.JS**  
   安裝長期穩定版\(LTS\) \[[官網連結](https://nodejs.org/en/)\]

   要查看安裝版本，打開命令提示字元\(CMD\)，輸入「`node -v`」

2. **安裝SASS** 在命令提示字元\(CMD\)輸入「`npm install -g sass`」 如果你用mac要輸入「`sudo npm install -g sass`」 更多詳情請見SASS\[[官網](https://sass-lang.com/install)\] 要查看安裝版本，命令提示字元\(CMD\)，輸入「`sass --version`」
3. VS code 安裝「**Live Sass Compiler**」  
   有像瀏覽器的console可以幫你查看哪裡有錯。  
   在vs code的JSON指令加上以下指令

   ```text
   "liveSassCompile.settings.formats": [
           {
               "format": "expanded",
               "extensionName": ".css",
               "savePath": "/css/"
           }
       ],
   ```



