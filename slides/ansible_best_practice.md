class: center,middle
# Ansible best practiceをやってみる

---
class: center,middle
# @douhashi

---
# Ansible とは

- https://www.ansible.com/
- (みなさんご存知)pythonで書かれた構成管理ツール。

---
# なにができるの？

- サーバ設定の自動化
- ネットワーク自動化
- クラウド(AWS/GCP)のプロビジョニング
- アプリケーションのデプロイ

---
# chef, puppetと何が違うの？

- SSHだけあればいい(管理される側にエージェント不要)
- yamlで書ける(シェルスクリプトに近くて受け入れやすい)
- **自分でplaybook(chefでいうレシピ)を書いていくスタンス**

---
# つまり

- (エージェントレスだから)既存のサーバでもすぐ使い始められる
- yamlで書くから、非エンジニアでもある程度見れる(かな？)
- 自分でplaybook書く系だから「**レシピ陳腐化してて動かない**」が少ない

---
class: center,middle
# でも、使ってみるといろいろある

---
# ansibleつまづきポイント

- ディレクトリ構造の正解がわからない
- role(playbookの分割単位)がまちまちになる
- 設定値はどこにおいたらいいの？
- production/staging/develop環境はどう分ける？

---
class: center,middle
# 自由すぎて、正解がわからない！！

---
# そんなansiblerのために、、、

Ansible Best Practiceってのがあるよ。


---
class: center,middle
# ちょっとだけ触ってみる

---
# こんな感じのサーバを作る

- nginx で、適当な感じのHTMLをserveするサーバ作る

---
# install ansible (on ubuntu)

```
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

※ 他はansibleのdoc見て

---
# インベントリファイルの作成

```
$ mkdir ~/workspace/tekitou_web
$ cd ~/workspace/tekitou_web
$ echo "サーバのIP" > inventory
```

※あと、対象サーバにsshつなげるように~/.ssh/configしとく

---
# playbook書く

```
$ vim playbook.yml
```

```

```
