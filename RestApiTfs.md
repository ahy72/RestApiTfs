name: inverse
layout: false
class: center, middle, inverse

<!-- github Web ページ https://qiita.com/budougumi0617/items/221bb946d1c90d6769e9 -->
---
# REST API for TFS

---
## TFS とは？

* TFS = Team Foundation Server  
ご存知の通り、ソースコードのバージョン管理システム

---
## REST API とは？

* REST = REpresentational State Transfer  
* API = Application Programming Interface

>Webシステムを外部から利用するためのプログラムの呼び出し規約(API)  
>RESTと呼ばれる設計原則に従って策定されたもの  

引用：[IT用語辞典 e-Words](http://e-words.jp/w/RESTful_API.html)  

HTTP の GET や POST で操作し、データのやり取りを JSON などで行うという程度のイメージでOK

---
## 目標

C# で REST API を用いて TFS を操作するまでの流れを知る  
今回は例としてビルドを実行してみる

---
## 準備①
### Visual Studio プロジェクトを用意  

[_demo_](#demo1)

---
### コンソールのプロジェクトを作成
![](image/project.png)

---
## nuget で Json パッケージを取得
![](image/nuget.png)  
```
PM> Install-Package Newtonsoft.Json
```
<a id="demo1"></a>
## 準備②
### アクセストークンの追加  
参考：[Authenticating with personal access tokens](https://docs.microsoft.com/en-us/azure/devops/integrate/get-started/authentication/pats?view=tfs-2018)
[_demo_](#demo2)

---
### TFS のアクセストークンページを開く

例  
http://_ServerName:8080_/tfs/_details/security/tokens

---
### [追加] をクリックする  
![](image/add.PNG)

---
### [説明] を任意で入力する  
![](image/setting1.PNG)

---
### [選択されたスコープ] を選択する  
![](image/setting2.PNG)

---
### [ビルド (読み取りおよび実行)] にチェックを入れる  
![](image/setting3.PNG)

---
### [トークンの作成] ボタンをクリックする
作成されたトークンは忘れずにコピーすること

---
<a id="demo2"></a>

---
class: center, middle, inverse
# おまけ

---
## Sourcetree

GitのGUIツール。使いやすいらしい(使ったことない)

<https://www.sourcetreeapp.com/>