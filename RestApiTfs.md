name: inverse
layout: true
class: center, middle, inverse
---
# Git入門

---
layout: false

## 対象者

* git未経験
* 基本的なコマンド操作可能

---
## 目標

* 基本的なgitコマンド操作ができるようになる  
* githubの操作ができるようになる

---
## Gitとは

* 変更履歴を記録・追跡するためのバージョン管理システム  
* ローカル環境で操作  
* 差分ではなくスナップショット  

---
## 用語

### リポジトリ
ファイルやディレクトリの状態を記録する場所。リモートリポジトリとローカルリポジトリがある


---
## インストール

[公式サイト](https://git-scm.com/downloads)よりダウンロード

![download](download.png)

---
インストールが完了すると、gitコマンドが使用可能になる

```console
# バージョン確認
$ git version
git version 2.19.1.windows.1

# ヘルプ表示
$ git --help
```

---
class: center, middle, inverse
# gitコマンド

---
## 覚えるべきgitコマンド(ローカル)

* init
* add
* commit

---
## git init

空のgitリポジトリを作成

```console
$ mkdir sample
$ cd sample
$ git init
```

![init](init.png)

---
## git add

ファイルをバージョン管理対象として追加する

```console
$ echo sample > sample.txt
$ git add sample.txt
```

全ファイルを追加したい場合

```console
$ git add .
```

---
## git commit

変更内容をリポジトリに追加する

```console
$ git commit -m "comment"
```

---
class: center, middle, inverse
# githubの利用

---
## アカウント作成
[公式サイト](https://github.com/)

![github_signup](github_signup.png)

---
## リポジトリの作成

<https://github.com/new>

![github_new](github_new.png)

---
作成したリポジトリのパスをコピー

![github_path](github_path.png)

---
class: center, middle, inverse
# gitコマンド2

---
## 覚えるべきgitコマンド(リモート)

* remote
* push
* pull
* clone

---
## git remote
リモートリポジトリの操作を行う

```console
# リモートリポジトリを追加
$ git remote add origin [リポジトリのパス]

# 登録されているリモートリポジトリの確認
$ git remote -v
origin  https://github.com/Kyohei-M/sample.git (fetch)
origin  https://github.com/Kyohei-M/sample.git (push)
```

---
## git push
リモートリポジトリにコミットをプッシュする

```console
$ git push origin master
```

![github_push](github_push.png)

---
## git pull

リモートリポジトリと同期する

```console
$ git pull origin master
```

---
## git clone
リポジトリをローカルに複製する

```console
$ git clone [リモートリポジトリのパス]
```

![github_clone](github_clone.png)

---
class: center, middle, inverse
# 注意点

---
## githubとsshキー
githubの操作には、ローカルマシンのsshキーを設定する必要がある

![github_ssh](github_ssh.png)

---
## sshキーの作成
参考サイト  
<https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html>

```console
$ ssh-keygen -t rsa -C "your_email@example.com"
```

作成される".ssh\id_rsa.pub"の中身をgithubにコピー

---
class: center, middle, inverse
# おまけ

---
## Sourcetree

GitのGUIツール。使いやすいらしい(使ったことない)

<https://www.sourcetreeapp.com/>

---
class: center, middle, inverse
# 皆さん、Gitを使いましょう！

---
## 参考  
公式サイト  
<https://git-scm.com/>

Wikipedia  
<https://ja.wikipedia.org/wiki/Git>