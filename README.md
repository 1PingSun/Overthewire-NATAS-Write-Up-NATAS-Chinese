# NATAS Write-up（NATAS 中文解答）

## [NATAS 0](http://natas0.natas.labs.overthewire.org)
> - Link: http://natas0.natas.labs.overthewire.org
> - Username: natas0
> - Password: natas0

1. 打開網頁原始碼，即可看到 NATAS 1 的密碼。

## [NATAS 1](http://natas1.natas.labs.overthewire.org)
> - Link: http://natas1.natas.labs.overthewire.org
> - Username: natas1
> - Password: 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq

1. 這題禁止使用右鍵，所以打不開開發者工具，可以用以下兩種方法開啟開發者工具：
    - 按鍵盤上的 F12 鍵打開開發者工具
    - 點擊瀏覽器右上角的三個點 > More Tools > Developer Tools

2. 打開後就會看到 NATAS 2 的密碼了。

## [NATAS 2](http://natas2.natas.labs.overthewire.org)
> - Link: http://natas2.natas.labs.overthewire.org
> - Username: natas2
> - Password: TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI

1. 在 Developer Tools 中的 Sources 分頁可以看到一個 `files` 的資料夾，當中只有一個 `pixel.png` 的檔案，故思考 `files` 資料夾中是否有其他檔案。
2. 在網址列後方加入 `/files` 變成 `http://natas2.natas.labs.overthewire.org/files` 後，發現還有一個 `users.txt` 的檔案。
3. 點擊打開 `users.txt` 後，就看到 NATAS 3 的密碼了。

## [NATAS 3](http://natas3.natas.labs.overthewire.org)
> - Link: http://natas3.natas.labs.overthewire.org
> - Username: natas3
> - Password: 3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
1. 打開原始碼後看到 `<!-- No more information leaks!! Not even Google will find it this time... -->`。
2. 不讓 Google 搜尋顯示網站的方法有兩種：

    參考文獻：https://www.da-vinci.com.tw/tw/blog/robots_noindex
    
    - 在原始碼加入 noindex
    - 撰寫跟目錄的 `robots.txt` 限制爬取資料
    
3. 猜測 NATAS 4 的在 `robots.txt` 中。
4. 在網址後方加入 `/robots.txt`，變成 `http://natas3.natas.labs.overthewire.org/robots.txt`。
5. 看到路徑 `/s3cr3t/` 被禁止存取。
6. 故前往 `/s3cr3t/`，變成 `http://natas3.natas.labs.overthewire.org/s3cr3t/`，並看見一個 `users.txt` 的檔案。
7. 點開 `users.txt` 後，就得到 NATAS 4 的密碼了。

## [NATAS 4](http://natas4.natas.labs.overthewire.org)
> - Link: http://natas4.natas.labs.overthewire.org
> - Username: natas4
> - Password: QryZXc2e0zahULdHrtHxzyYkj59kUxLQ

1. 網頁顯示僅允許來自 `http://natas5.natas.labs.overthewire.org/` 的使用者存取。
2. 打開 Developer Tools 的 Network 分頁後，看到 `index.php` 封包中有一個 `Host` 標籤，透過 [`ModHeader`](https://chromewebstore.google.com/detail/modheader-modify-http-hea/idgpnmonknjnojddfkpgkljpfnnfcklj) 等工具，將 `Referer` 的內容改成 `http://natas5.natas.labs.overthewire.org/`，點擊網頁中的 `Refresh page`，即可看到 NATAS 5 的密碼。

## [NATAS 5](http://natas5.natas.labs.overthewire.org)
> - Link: http://natas5.natas.labs.overthewire.org
> - Username: natas5
> - Password: 0n35PkggAPm2zbEpOU802c0x0Msn1ToK

1. 網頁顯示沒有登入。
2. 打開 Developer Tools 的 Application 分頁，看到 Cookie 中有一個 `loggedin` 的值為 `0`。
3. 雙擊 `loggedin` 的值，並修改成 `1` 後，重新整理就看到 NATAS 6 的密碼了。

## [NATAS 6](http://natas6.natas.labs.overthewire.org)
> - Link: http://natas6.natas.labs.overthewire.org
> - Username: natas6
> - Password: fOIvE0MDtPTgRhqmmvvAOt2EfXR6uQgR

1. 點擊 `View sourcecode`後，打開網頁後端原始碼。
2. 發現要讓網頁吐出 NATAS 7 密碼的方式，就是讓 `$secret` 與 `$_POST['secret']` 的內容相符。也就是說：網頁中輸入框的文字必須與 `$secret` 相符。
3. 在後端原始碼中找了一下，發現找不到 `$secret` 的宣告或賦值指令，故推測該值為後端原始碼中的 `include "includes/secret.inc";` 代入的。
4. 回到前端網頁，在網址列後方加入 `/includes/secret.inc`，就看到 `$secret` 的值為 `FOEIUWGHFEEUHOFUOIU`。
5. 在網頁輸入框中，輸入 `$secret` 的值：`FOEIUWGHFEEUHOFUOIU`。
6. 就得到 NATAS 7 的密碼了。
    
## [NATAS 7](http://natas7.natas.labs.overthewire.org)
> - Link: http://natas7.natas.labs.overthewire.org
> - Username: natas7
> - Password: jmxSiH3SP6Sonf8dv66ng8v1cIEdjXWr

1. 點擊 `Home` 或 `About` 後，發現連結中的 `page` 參數會隨之改變。
2. 嘗試改變 `page` 參數後，會發現顯示錯誤訊息：找不到這樣的路徑。
3. 回到官網：[`OverTheWire`](https://overthewire.org/wargames/natas/)，看到密碼均存在 `/etc/natas_webpass/natas?`（`?` 是題號的數字，例如：NATA 7 的密碼就存在 `/etc/natas_webpass/natas7`）
4. 回到 NATAS 7，在網址列中的 `page` 參數修改成 `/etc/natas_webpass/natas8` 後，就得到 NATAS 8 的密碼了。

## [NATAS 8](http://natas8.natas.labs.overthewire.org)
> - Link: http://natas8.natas.labs.overthewire.org
> - Username: natas8
> - Password: a6bZCNYwdKqN5cGP11ZdtPg0iImQQhAB

1. 點擊 `View soursecode` 查看後端 php 原始碼。
2. 有一個函式 `encodeSecret()` 會將輸入的值，經過以下處理並回傳：

    1. 進行 Base64 編碼
    2. 將字串反轉
    3. 將二進位轉換成十六進位
3. 查看主函式發現讓輸入框中的文字經過 `encodeSecret()` 函式計算後，只要與 `$encodedSecret` 相等，就能得到 NATAS 9 的密碼。
4. 想達成上一點的條件，就需要將 `$encodedSecret` 變數的文字反向解碼，以下是解碼的步驟：

    1. 十六進位轉二進位
    2. 字串反轉
    3. Base64 解碼
5. 將上一點的解碼 `oubWYf2kBq` 貼上輸入框並送出，就得到 NATAS 9 的密碼了。
## [NATAS 9](http://natas9.natas.labs.overthewire.org)
> - Link: http://natas9.natas.labs.overthewire.org
> - Username: natas9
> - Password: Sda6t0vkOPkM8YeOZkAGVhFoaplvlJFd

1. 打開網頁 php 原始碼，看到 `passthru()` 函式，這個函式可以執行任何 shell 指令。
2. 由程式碼可看出，該行程式會在 `dictionary.txt` 中尋找字串，而尋找的字串即為輸入框輸入的值。
3. 可以使用 `;` 分開多個執行指令，所以在輸入框的輸入值前後各加入一個 `;`，就能執行任意指令了！
5. 使用 `cat /etc/natas_webpass/natas10` 指令即可讀取 `/etc/natas_webpass/natas10` 檔案的內容。
6. 在輸入框中輸入 `;cat /etc/natas_webpass/natas10;`，就得到 NATAS 10 的密碼了。

## [NATAS 10](http://natas10.natas.labs.overthewire.org)
> - Link: http://natas10.natas.labs.overthewire.org
> - Username: natas10
> - Password: D44EcsFkLxPIkAAKLosx8z3hxX1Z4MCE

1. 在這關中，因為禁止了一些字元的輸入，所以無法像 NATAS 9 一樣利用分號隔開指令，並任意執行。
2. 但仍可用正規表達式中的 `.*` 輸出檔案中的所有內容。
3. 在輸入框中輸入 `".*" /etc/natas_webpass/natas11` 後，就在輸出的第一行得到 NATAS 11 的密碼了。

## [NATAS 11](http://natas11.natas.labs.overthewire.org)
> - Link: http://natas11.natas.labs.overthewire.org
> - Username: natas11
> - Password: 1KFqoJXi6hRaPluAmk8ESDW4fSysRoIg

1. 觀察原始碼，以下是原始碼之邏輯流程圖。

```mermaid
graph TD;
    subgraph loadData Function
        A([開始]);
        A --> B{篩選各種不是很重要的判斷式};
        B -- Yes --> C[/讀取 Cookie 中 $data 值/];
        C --> D[對其進行 Base64 解密];
        D --> E[對其再進行 XOR 運算（尚不知道 Key 值）];
        E --> F[將其 JSON 格式轉換成 Array];
        F --> J[/回傳解碼後之值/]
        B -- No --> G[/回傳預設值/];
    end
    subgraph 設定背景色
        G --> H[將 Cookie 中 $data 的背景色值，設定成前端輸入框的值];
        J --> H;
    end
    subgraph 回傳 Cookie
        H --> I[/讀取 $data 解密後的值/];
        I --> K[將其 Array 格式轉換成 JSON 格式];
        K --> L[對其進行 XOR 運算（與 loadData Function 的 Key 值相同）];
        L --> M[對其進行 Base64 加密];
        M --> N[/回傳至前端編碼後的 Cookie/];
    end
    subgraph 顯示 NATAS 12 之密碼
        N --> O{判斷 $data 中的 showpassword 值是否為 yes};
        O -- Yes --> P[/回傳 NATAS 12 密碼並顯示在前端/];
    end
    O -- No --> Q([結束]);
    P --> Q; 
```

2. 由上流程圖可知將 Cookie 中 data 的 showpassword 值設定為 yes 即可獲得 NATAS 12 的密碼。
3. 在將 showpassword 的值設定成 yes 之前，必須先得知 XOR 的 Key。
4. 目前 Cookie 中的 data 值為預設的值，所以我們可以將以下兩物件進行 XOR 運算，即可得到 Key。
    1. 預設值轉換成 JSON 格式
    2. data 值進行 Base64 的解密
5. 可透過以下程式獲得預設值的 JSON 格式。
    ```
    <?php
        $a = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");
        echo json_encode($a);
    ?>
    ```
6. 獲得預設值的 JSON 格式為：`{"showpassword":"no","bgcolor":"#ffffff"}`。
7. 將 Cookie 中 data 值進行 Base64 解密後，得到：`0l;$$98-8=?#9*jvi 'ngl*+(!$#9lrnh(.*-(.n67`。
8. 將其進行 XOR 運算後得到 Key 為：`KNHL`，可透過稍作修改該網頁至 php 原始碼進行 XOR 運算，範例程式如下：
    ```
    <?php
        $text1 = '{"showpassword":"no","bgcolor":"#ffffff"}';
        $text2 = "0l;$$98-8=?#9*jvi 'ngl*+(!$#9lrnh(.*-(.n67";
        $key = '';
        
        for($i=0;$i<strlen($text1);$i++) {
            $key .= $text1[$i] ^ $text2[$i % strlen($text1)];
        }
        
        echo $key;
    ?>
    ```
9. 將 `{"showpassword":"yes","bgcolor":"#ffffff"}` 與 Key 值：`KNHL` 進行 XOR 運算後，得到運算結果為：`0l;$$98-8=?#9*jvi7-?ibj.,-' $<jvim.*-(.*i3`。
10. 將 XOR 運算後的值進行 Base64 編碼得到：`MGw7JCQ5OC04PT8jOSpqdmk3LT9pYmouLC0nICQ8anZpbS4qLSguKmkz`。
11. 將其設定為 Cookie 的 data 值後重新整理，就得到 NATAS 12 的密碼了！恭喜你完成了一個困難的任務 XD。
   
## [NATAS 12](http://natas12.natas.labs.overthewire.org)
> - Link: http://natas12.natas.labs.overthewire.org
> - Username: natas12
> - Password: YWqo0pjpcXzSIl5NMAVxg12QxeC1w9QG

## [NATAS 13](http://natas13.natas.labs.overthewire.org)
> - Link: http://natas13.natas.labs.overthewire.org
> - Username: natas13
> - Password: lW3jYRI02ZKDBb8VtQBU1f6eDRo6WEj9

## [NATAS 14](http://natas14.natas.labs.overthewire.org)
> - Link: http://natas14.natas.labs.overthewire.org
> - Username: natas14
> - Password: qPazSJBmrmU7UQJv17MHk1PGC4DxZMEP

## [NATAS 15](http://natas15.natas.labs.overthewire.org)
> - Link: http://natas15.natas.labs.overthewire.org
> - Username: natas15
> - Password: TTkaI7AWG4iDERztBcEyKV7kRXH1EZRB

## [NATAS 16](http://natas16.natas.labs.overthewire.org)
> - Link: http://natas16.natas.labs.overthewire.org
> - Username: natas16
> - Password: TRD7iZrd5gATjj9PkPEuaOlfEjHqj32V
