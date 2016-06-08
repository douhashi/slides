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
# ansible用語

- playbook
  - 操作手順を書いたもの(=レシピ)。YAMLで書く。
- role
  - ある程度のまとまりでplaybookを区切ったもの
  - ex) rbenvを入れる rbenv ロール
- vars
  - インストールするバージョンとか、パラメータ的なものを書くスペース。YAML。
- inventory
  - 管理するサーバの接続先をまとめて書く(=hostsみたいなの)
  - iniファイル形式っていうのかな？で書く

---
class: center,middle
# サンプルを見せる時間

---
class: center,middle
# でも、使ってるといろいろ悩む

---
# ansibleつまづきポイント

- ディレクトリ構造の正解がわからない
- role(playbookの分割単位)がまちまちになる
- 設定値はどこにおいたらいいの？
- production/staging/develop環境はどう分ける？

---
class: center,middle
# 自由すぎて、正解がわからない

---
# そんなansiblerのために、、、

Ansible Best Practiceってのがあるよ。

- http://docs.ansible.com/ansible/playbooks_best_practices.html

---
class: center,middle
# かいつまんで、まとめてみる

---
class: center,middle
# inventory

---
- inventory はグルーピングをうまく使う
- best practice的には [場所]と[役割]でまとめる

```
[ap-north-east-webservers]
↑場所 & 役割

[ap-north-east-dbservers]
↑場所 & 役割

[webservers:children]
ap-north-east-webserver
↑役割でまとめる

[dbservers:children]
ap-north-east-dbservers
↑役割でまとめる

[ap-north-east:children]
ap-north-east-webservers
ap-north-east-dbservers
↑場所でまとめる
```

---
# role

- roleの分割単位を細かくしすぎない！
- roleはroleって名前だけど、includeの単位
  - それ「role」って名前適切なの？って議論もある
- best practiceは common/webtier/dbtierの3つ
- 長くなったら分割する

---
# vars

- group_vars, host_varsを駆使する
  - group_vars => webtierだけに適用するvars
  - host_vars => 単一ホストに適用するvars
    - ex) host Aはsmallインスタンスだからunicorn worker 2つまで、とか
