- [実質無料で使える Hosting Service の比較や使い分けの紹介 2021 (Firebase Hosting, Cloudflare Pages, Vercel, Netlify, GitHub Pages, Amplify, CloudRun)](https://blog.ojisan.io/hosting-battle-2021/)
- [ずっと無料で使えるクラウドの「Free Tier」主要サービスまとめ。2021 年版 － Publickey](https://www.publickey1.jp/blog/21/free_tier2021.html)
- [S3 互換オブジェクトストレージまとめ](https://zenn.dev/voluntas/scraps/a0f0890c195798)
- [個人開発を黒字にする技術](https://k0kubun.hatenablog.com/entry/surplus)
- [RailsアプリをHerokuから移行するならどれがいいのか比較する](https://blog.unasuke.com/2022/compare-heroku-alternatives/)

## [Heroku](https://www.heroku.com/)

- 安裝
  - node.js 版本須 > 8
  - 須安裝 npm
  - [Getting Started on Heroku with Node.js](https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up)
- 登入
  - `heroku login`
- 部署
- 創建 Git 與連結 App
-

```bash
  git init
  git add .
  git commit -m 'first commit'

  heroku create [app-name]
  heroku git:remote -a [app-name]

  git push heroku master
```

- heroku 需要 start 指令才可建置專案，因此需於 `package.json` 裡加入:

```json
  "scripts": {
    "test": echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
```

- 修改專案名稱: `heroku apps:rename --app [old-name] [new-name]`
- 檢視遠端連結: `git remote -v`
- 設置 MySQL

```bash
  heroku addons:create cleardb:ignite
  heroku config | grep CLEARDB_DATABASE_URL
```

## [Netlify](https://www.netlify.com/)

## [Vercel](https://vercel.com/)

## [Firebase](https://firebase.google.com/)

- [Firebase console](https://console.firebase.google.com/u/0/)
- BaaS (Backend as a Service)
- [介紹](https://qiita.com/uhooi/items/aa6945a5da5dd6172d2b)
  - 1. [Cloud Firestore](https://firebase.google.com/products/firestore)
    - NoSQL Database
  - 2. [Cloud Functions](https://firebase.google.com/products/functions)
    - 執行 serverless back-end code
  - 3. [Authentication](https://firebase.google.com/products/auth)
    - 認證系統
    - 實裝登入功能
  - 4. [Hosting](https://firebase.google.com/products/hosting)
    - Web Hosting
    - 實裝 LP、PWA
  - 5. [Cloud Storage](https://firebase.google.com/products/storage)
    - 雲端外部存放空間
    - 儲存與提供圖片、影片檔案
  - 6. [Realtime Database](https://firebase.google.com/products/realtime-database)
    - NoSQL Database
    - 一般會選用 Firestore
    - 差異參照：[選擇一個數據庫：Cloud Firestore 或實時數據庫](https://firebase.google.com/docs/database/rtdb-vs-firestore)
  - 7. [Crashlytics](https://firebase.google.com/products/crashlytics)
    - 檢視錯誤
  - 8. [Performance Montioring](https://firebase.google.com/products/performance)
    - 計測效能
  - 9. [Test Lab](https://firebase.google.com/products/test-lab)
    - 裝置測試
    - UI 測試、Monkey Test
  - 10. [Google Analytics](https://firebase.google.com/products/analytics)
    - 分析使用者
  - 11. [Predictions](https://firebase.google.com/products/predictions)
  - 12. [Cloud Messaging](https://firebase.google.com/products/cloud-messaging)
    - 推送通知
  - 13. [Remote Config](https://firebase.google.com/products/remote-config)
    - 遠端變更 App 設定
    - 期間限定外觀、A/B Test
  - 14. [Dynamic Links](https://firebase.google.com/products/dynamic-links)
    - Deep Link
    - 生成一連結，讓使用者已安裝則啟動 App，未安裝則移動至 Store
- [使用](https://qiita.com/iiizoo/items/a31726966c1a42f37809)
  - 1. 新建 Project
  - 2. 從左上齒輪設定 Soruce Location
  - 3. 新增 App
  - 4. `npm i -g firebase-tools`
  - 5. 移動至作業資料夾
  - 6. `npm i --save firebase`
  - 7. `firebase login`
  - 8. `firebase init`
  - 9. `firebase deploy`

## GCP

- [利用 Cloud function 製作 GitHub Apps](https://blog.techbridge.cc/2020/06/21/github-apps-cloudfunction/)
- [個人開発激安 GCP (にしたい)](https://zenn.dev/suyaa/articles/93b23462b08e95)

## [Amazon AWS Free Plan](https://aws.amazon.com/tw/)

- AWS Lambda
  - [Serverless 架構應用開發指南 - serverless](https://serverless.ink/)
  - [使用 Node.js + serverless framework + AWS Lambda 打造可擴展、更穩定而且更經濟的架構](https://medium.com/visuallylab/%E4%BD%BF%E7%94%A8-node-js-serverless-framework-aws-lambda-%E6%89%93%E9%80%A0%E5%8F%AF%E6%93%B4%E5%B1%95-%E6%9B%B4%E7%A9%A9%E5%AE%9A%E8%80%8C%E4%B8%94%E6%9B%B4%E7%B6%93%E6%BF%9F%E7%9A%84%E6%9E%B6%E6%A7%8B-6a54b51b8988)
- Amazon DynamoDB
- [基本的なシステム構成図を理解するための AWS 基礎をまとめてみた](https://qiita.com/goldayushi/items/0e0f34d19813b8fdc2b8)
- [2020 AWS によるクラウド入門](https://tomomano.gitlab.io/intro-aws/)
- [2021 コードで学ぶ AWS 入門](https://tomomano.github.io/learn-aws-by-coding/)
- [AWS アカウントを作ったら最初にやるべきこと 〜2021 年版〜 #devio2021 | DevelopersIO](https://dev.classmethod.jp/articles/aws-1st-step-2021/)
- [AWS が落ちても GCP に逃がすことで落ちないシステムを作る技術](https://tech.plaid.co.jp/karte-blocks-multicloud/)

## Microsoft Azure

- Azure App Service
- Azure Functions
- Azure DevOps

## Oracle Cloud

## IBM Cloud
