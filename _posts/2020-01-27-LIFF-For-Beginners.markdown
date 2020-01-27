---
layout: post
title: LIFF For Beginners
date: 2020-01-27
description: LINE Front-end Framework (LIFF) is a platform for web apps provided by LINE. The web apps running on this platform are called LIFF apps. # Add post description (optional)
img: "LIFF/LIFF.jpg" # Add image post (optional)
tags: [LIFF, LineBot, notes] # add tag
---

### Introduction to LINE Front-end Framework (LIFF)

* LIFF 是一種讓使用者在 LINE APP 中開啟網頁應用程式。

	<img src="./../assets/img/LIFF/LIFF-intro.jpg" width="600">
	* 特色：

		1. 使用者能直接在 LINE 中開啟網頁，而不用跳出 LINE 後，再從另開的瀏覽器中看到網頁內容。
		2. 在 LINE 中開啟網頁能直接取得 LINE 使用者的資料。
	
	* 開啟的網頁能設定 3 種高度：Compact / Tall / Full

		![LIFF intro](./../assets/img/LIFF/LIFF-size.jpg)
	
	* 相關應用：

		1. [LINE LIFF 你畫我猜](https://feifacunzai.github.io/2018/09/05/LINE-LIFF-%E4%BD%A0%E7%95%AB%E6%88%91%E7%8C%9C/)
		2. [「Dr.穀雨」 智慧照顧機器人](https://chibupapa.com/2019/05/14/line-liff/)
		3. [傳送手繪圖 (原始版)](https://engineering.linecorp.com/en/blog/liff-our-latest-product-for-third-party-developers/) / [傳送手繪圖 (改良版)](https://medium.com/@danielkao/%E5%88%9D%E6%8E%A2-line-message-api-%E7%9A%84%E6%96%B0%E5%8A%9F%E8%83%BD-liff-51d5e7ff1a6a)

### Tutorial (Local Testing)

1. **Go to [LINE developer 帳戶](https://developers.line.biz/en/)**

	* Create a new provider
	* Create a Messaging API channel
	* Fill in the field in `Basic settings`
	* In `Messaging API`, click the `issue` in `Channel access token`

2. **Go to [LINE 官方 GitHub](https://github.com/line/line-liff-v2-starter)**

	* Open Command Line 

		```
		$ git clone https://github.com/line/line-liff-v2-starter
		$ cd line-liff-v2-starter
		$ npm install dotenv --save
		$ node index.js
		```

	* Modify: Add the environment variable

		* `index.js`
			
			```javascript
			const express = require('express');
			const app = express();
			const port = process.env.PORT || 5000;

			require('dotenv').config(); 			//Add
			const myLiffId = process.env['MY_LIFF_ID'];	//Modyify

			app.use(express.static('public'));
			app.get('/send-id', function(req, res) {
			    res.json({id: myLiffId});
			});

			app.listen(port, () => console.log(`app listening on port ${port}!`));
			```

		* `.env`

			```
			MY_LIFF_ID=<Enter_LIFF_ID>
			```

			=> Go to [LINE 官方 GitHub](https://github.com/line/line-liff-v2-starter) > LIFF > LIFF URL

			```
			LIFF URL	line://app/<HERE_IS_LIFF_ID>
			```


3. Add LIFF in [LINE developer 帳戶](https://developers.line.biz/en/)

	* Fill in the field in `LIFF`
		* LIFF app name
		* Size
		* Endpoint URL -> Step 4. will fill in!
		* Scopes -> all check


4. **Install ngrok and Open Command Line**

	* `$ ngrok.exe http 5000`
	* Copy `https://e0c27532.ngrok.io`, and paste to [LINE developer 帳戶](https://developers.line.biz/en/) > LIFF `Endpoint URL`

5. Finish!
	
	<img src="./../assets/img/LIFF/Screenshot_2020-01-27-13-57-01-04.png" width="300px">
	&emsp;
	<img src="./../assets/img/LIFF/Screenshot_2020-01-27-13-57-57-01.png" width="300px">

---
### Reference Source

* [LINE Developers: LIFF v2](https://developers.line.biz/en/docs/liff/overview/)
* [Line 官方 GitHub: LIFF v2 starter app](https://github.com/line/line-liff-v2-starter)
* [LIFF v1 (LINE Front-end Framework) 實作教學](https://medium.com/harry-xies-blog/line-front-end-framework-liff-%E5%AF%A6%E4%BD%9C%E6%95%99%E5%AD%B8-3f810c96c17d)

### Supplement

* [LIFF v2 新增支援外部瀏覽器與二維條碼掃描器等功能](https://engineering.linecorp.com/zh-hant/blog/liff-our-latest-product-for-third-party-developers-ch/)