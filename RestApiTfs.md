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

>Webシステムを外部から利用するためのプログラムの呼び出し規約(API)  
>RESTと呼ばれる設計原則に従って策定されたもの  

引用：[IT用語辞典 e-Words](http://e-words.jp/w/RESTful_API.html) 

* REST = REpresentational State Transfer  
* API = Application Programming Interface

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

---
## 参照が追加されていることを確認  
![](image/json.png)  

---
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
## 準備③
### ビルド定義を作成

例  
http://_ServerName:8080_/tfs/_CollectionName_/_ProjectName_/_build

---
### 今回は省略
ビルド定義は既に作ってあるものとする  
継続的インテグレーションだったり、デイリービルドでの単体テスト実行だったりの設定が書かれている

---

## 準備終わり

---
## ビルド実行までの流れ
1. HttpClient を作成する
1. ビルド定義の名称から、ビルド定義を検索する
1. 取得したビルド定義を実行する

---
### HttpClient を作成
``` cs
private static readonly HttpClient HttpClient;

HttpClient = new HttpClient();

HttpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

string authParameter = Convert.ToBase64String(Encoding.ASCII.GetBytes($":{PersonalAccessToken}"));
HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", authParameter);
```
PersonalAccessToken は準備②で用意したアクセストークンを指定する  
インスタンスは static で保持する  
参考：[不適切なインスタンス化のアンチパターン](https://docs.microsoft.com/ja-jp/azure/architecture/antipatterns/improper-instantiation/)

---
### ビルド定義を検索
リファレンスを見るとこう書かれている

>Get a list of builds  
>GET https://{instance}/DefaultCollection/{project}/_apis/build/builds?api-version={version} 以下略

引用：[Get a list of builds](https://docs.microsoft.com/en-us/azure/devops/integrate/previous-apis/build/builds?view=tfs-2018#get-a-list-of-builds) 

---
<font color="Red">https://{instance}/DefaultCollection/{project}</font>/_apis/build/builds?api-version={version}  
この<font color="Red">赤字</font>部分は環境によって読み替える  

例  
http://_ServerName:8080_/tfs/_CollectionName_/_ProjectName_

---
https://{instance}/DefaultCollection/{project}/_apis/build/builds?<font color="Red">api-version={version}</font>  
この<font color="Red">赤字</font>部分はTFSのバージョンと対応している

>|TFS Version|REST API Version|
>|:---|:---|
>|TFS 2017 Update 2|3.2|
>|TFS 2017 Update 1|3.1|
>|TFS 2017 RTW|3.0|
>|TFS 2015 Update 3|2.3|
>以下略

引用：[API and TFS version mapping](https://docs.microsoft.com/en-us/azure/devops/integrate/previous-apis/overview?view=tfs-2018#api-and-tfs-version-mapping) 
---
class: center, middle, inverse
# おまけ

---
## Sourcetree

GitのGUIツール。使いやすいらしい(使ったことない)

<https://www.sourcetreeapp.com/>