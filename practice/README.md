# practice

## gitのインストールからPull Request作成まで
- gitをインストールし、github.com にssh接続できるようになる
- 「hayasaki-shunsuke(自分のアカウント)/github-test」を作成する
- 「hayapi(自分のアカウント).md」を追加するPull Requestを作成する

# 手順

## gitをインストールします。
- Windows：[https://prog-8.com/docs/git-env-win](https://prog-8.com/docs/git-env-win)
- Mac：[https://tracpath.com/bootcamp/git-install-to-mac.html](https://tracpath.com/bootcamp/git-install-to-mac.html)
## VSCodeをインストールします。
- [https://code.visualstudio.com/](https://code.visualstudio.com/)
## [github.com](http://github.com) のアカウントを作成します。
- [https://github.com/](https://github.com/)
## [github.com](http://github.com) にSSH接続できるようにする
- 公開鍵を作って、github.com に登録する
- 参考記事：[https://qiita.com/unsoluble_sugar/items/14bea376d8e6fce82eb3](https://qiita.com/unsoluble_sugar/items/14bea376d8e6fce82eb3)

- Windowsの場合「Git Bash」
![image](https://user-images.githubusercontent.com/48468109/117159359-2be8b680-adfb-11eb-931e-3eca1144d625.png)
- Macの場合「ターミナル」 
![image](https://user-images.githubusercontent.com/48468109/117159265-18d5e680-adfb-11eb-9637-1b5cf279c8a5.png)

```bash
## ~/.ssh がない場合はディレクトリを作成する
[hayasaki-shunsuke@PMAC873S] ~
## pwd カレントディレクトリを表示
% pwd
/Users/hayasaki-shunsuke
[hayasaki-shunsuke@PMAC873S] ~
## mkdir ディレクトリを作成する
% mkdir ~/.ssh

## .ssh が作成されていることを確認
% pwd
/Users/hayasaki-shunsuke/.ssh

[hayasaki-shunsuke@PMAC873S] ~
% cd ~/.ssh
[hayasaki-shunsuke@PMAC873S] ~/.ssh
## ssh-keygen sshの秘密鍵と公開鍵のキーペアを作成する
% ssh-keygen -t rsa
Generating public/private rsa key pair.
## id_git_rsa gitで使用する鍵の情報なのでわかりやすくするために「id_git_rsa」に名称変更
Enter file in which to save the key (/Users/hayasaki-shunsuke/.ssh/id_rsa): id_git_rsa
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in id_git_rsa.
Your public key has been saved in id_git_rsa.pub.
The key fingerprint is:
SHA256:XXXXXXXXXXXXXXXXXX hayasaki-shunsuke@PMAC873S
The key's randomart image is:
+---[RSA 3072]----+
|     o**E+.      |
|    .oo+..       |
|   ...o o        |
|    ...+     . . |
|     .o+S   . ...|
|     .o.oo o  o.+|
|     +... + + .+o|
|    . o+ o + + ..|
|     .o . o+B+o  |
+----[SHA256]-----+

## id_git_rsa と id_git_rsa.pub が作成されていることを確認
[hayasaki-shunsuke@PMAC873S] ~/.ssh
% ls
config		id_git_rsa	id_git_rsa.pub	id_rsa		id_rsa.pub
```
- ~/.ssh/config ssh接続設定を記述するファイルを作成する
    - VSCode を使用する場合、`code  ~/.ssh/config` を実行しファイルを新規作成
    ```
    Host *
        AddKeysToAgent yes
        UseKeychain yes

    Host github github.com
        HostName github.com
        IdentityFile ~/.ssh/id_git_rsa
        User hayasaki-shunsuke
    ```
    - vim を使用する場合、 `vim ~/.ssh/config` を実行しファイルを新規作成
        - 参考資料：https://qiita.com/hide/items/5bfe5b322872c61a6896
    ```bash
    ## ~/.ssh/config ssh接続設定を記述するファイルを作成する
    [hayasaki-shunsuke@PMAC873S] ~
    ## vim ~/.ssh/config ファイルの内容を確認
    % vim ~/.ssh/config

    Host *
        AddKeysToAgent yes
        UseKeychain yes

    Host github github.com
        HostName github.com
        IdentityFile ~/.ssh/id_git_rsa
        User hayasaki-shunsuke
    ```

```bash
## 生成した秘密鍵に読み取り専用属性を与える
[hayasaki-shunsuke@PMAC873S] ~/.ssh
% chmod 600 id_git_rsa

[hayasaki-shunsuke@PMAC873S] ~/.ssh
% eval `ssh-agent`
Agent pid 85934

## ssh-agentに秘密鍵を登録
[hayasaki-shunsuke@PMAC873S] ~/.ssh
% ssh-add ~/.ssh/id_rsa
Enter passphrase for /Users/hayasaki-shunsuke/.ssh/id_rsa:

[hayasaki-shunsuke@PMAC873S] ~/.ssh
% ssh-add ~/.ssh/id_git_rsa
Enter passphrase for /Users/hayasaki-shunsuke/.ssh/id_git_rsa:
Identity added: /Users/hayasaki-shunsuke/.ssh/id_git_rsa (hayasaki-shunsuke@PMAC873S)

## 公開鍵をコピーする
[hayasaki-shunsuke@PMAC873S] ~/.ssh
## (Mac)pbcopy < ~/.ssh/id_git_rsa.pub クリップボードにコピー
## (Windows)clip < ~/.ssh/id_git_rsa.pub クリップボードにコピー
% pbcopy < ~/.ssh/id_git_rsa.pub
[hayasaki-shunsuke@PMAC873S] ~/.ssh
``` 
- [https://github.com/settings/ssh/new](https://github.com/settings/ssh/new)
    - 「Title」はPC名
    - 「Key」は[公開鍵をコピーする](#公開鍵をコピーする) でコピーした「id_git_rsa.pub」の内容
![image](https://user-images.githubusercontent.com/48468109/116080199-b7fc2f00-a6d3-11eb-85dc-7e20a8084ac2.png)
```bash
## github.com にssh接続できるか確認
% ssh -T git@github.com
Enter passphrase for key '/Users/hayasaki-shunsuke/.ssh/id_git_rsa':
Hi hayasaki-shunsuke! You've successfully authenticated, but GitHub does not provide shell access.
```
## github.com にアクセスしてブラウザからリポジトリを作成する
- 「hayasaki-shunsuke(自分のアカウント)/github-test」という名前のリポジトリ作成
    - [https://github.com/new](https://github.com/new)
    - `Add a README file` にチェック
    ![image](https://user-images.githubusercontent.com/48468109/116080303-da8e4800-a6d3-11eb-8bbd-2d44d4f32135.png)
    - [https://github.com/hayasaki-shunsuke/github-test](https://github.com/hayasaki-shunsuke/github-test)
    ![image](https://user-images.githubusercontent.com/48468109/116080360-ebd75480-a6d3-11eb-8907-4577bdaf7335.png)
## リポジトリをCloneして、VSCodeで開く
- [https://github.com/hayasaki-shunsuke/github-test](https://github.com/hayasaki-shunsuke/github-test)
    - 緑のCode をクリック
    - SSH を選択
    - コピーボタンをクリック
        - `git@github.com:hayasaki-shunsuke/github-test.git`
    ![image](https://user-images.githubusercontent.com/48468109/116080471-15907b80-a6d4-11eb-82c1-73a3bc53a8b3.png)

    ```bash
    ## ディレクトリ名を表示
    % pwd
    /Users/hayasaki-shunsuke

    ## mkdir Desktop/src ディレクトリを作成
    [hayasaki-shunsuke@PMAC873S] ~
    % mkdir Desktop/src

    ## Desktop/src に移動
    [hayasaki-shunsuke@PMAC873S] ~
    % cd Desktop/src

    ## git clone コマンドを実行してファイルをダウンロードする
    [hayasaki-shunsuke@PMAC873S] ~/Desktop/src
    % git clone git@github.com:hayasaki-shunsuke/github-test.git
    Cloning into 'github-test'...
    remote: Enumerating objects: 3, done.
    remote: Counting objects: 100% (3/3), done.
    remote: Compressing objects: 100% (2/2), done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Receiving objects: 100% (3/3), done.

    ## cloneした github-test のディレクトリに移動
    % cd github-test
    [hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (main)
    % ls
    README.md
    ```
## ブランチを作成する
- git branch hayapi
- git checkout hayapi
```bash
## branch を作成する
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (main)
% git branch hayapi
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (main)
## ブランチの一覧を確認、「hayapi」のブランチが作成されている
% git branch
hayapi
* main

## branchを切り替える（checkout）
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (main)
% git checkout hayapi
Switched to branch 'hayapi'
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
## ブランチが切り替わっていることを確認
% git branch
* hayapi
main
```
## ファイルを編集する
- touch hayapi.md
- code hayapi.md (hayapi.md をVSCodeで開く)
```bash
## ファイル確認
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
% ls
README.md

## ファイル作成
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
% touch hayapi.md
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
% ls
README.md	hayapi.md
```
```bash
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
% code hayapi.md

## hayapi
- hayapiのテストファイルです。
```
## コミットする
- git add hayapi.md
```bash
## git status ファイルの変更状況を確認
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
## git status 変更内容を確認
% git status
On branch hayapi
Untracked files:
(use "git add <file>..." to include in what will be committed)
hayapi.md

nothing added to commit but untracked files present (use "git add" to track)

## git add してステージングエリアに追加
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
% git add hayapi.md
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi) <S>
## git status 変更内容を確認
% git status
On branch hayapi
Changes to be committed:
(use "git restore --staged <file>..." to unstage)
new file:   hayapi.md
```
- git commit -m "hayapi.mdを追加"
```bash
## git commit ファイルの変更をコメント付きでコミットする
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi) <S>
% git commit -m "hayapi.mdを追加"
[hayapi 033c754] hayapi.mdを追加
1 file changed, 2 insertions(+)
create mode 100644 hayapi.md

[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
## git status 変更内容を確認
% git status
On branch hayapi
nothing to commit, working tree clean
```
## プッシュする
- git push --set-upstream origin hayapi
```bash
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
## git push コミットした内容をpushする
% git push
fatal: The current branch hayapi has no upstream branch.
To push the current branch and set the remote as upstream, use

git push --set-upstream origin hayapi

[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
## `--set-upstream origin hayapi` を指定してhayapi ブランチをプッシュする
## 参考資料:https://qiita.com/ponsuke0531/items/410735b544795506fdc5
% git push --set-upstream origin hayapi
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 343 bytes | 343.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'hayapi' on GitHub by visiting:
remote:  https://github.com/hayasaki-shunsuke/github-test/pull/new/hayapi
remote:
To github.com:hayasaki-shunsuke/github-test.git
* [new branch]  hayapi -> hayapi
Branch 'hayapi' set up to track remote branch 'hayapi' from 'origin'.
[hayasaki-shunsuke@PMAC873S] ~/Desktop/src/github-test (hayapi)
```
## PRを作る
- ブランチがプッシュされるとボタンが出る
![image](https://user-images.githubusercontent.com/48468109/116080588-3c4eb200-a6d4-11eb-8531-79cebf734eed.png)
- [https://github.com/hayasaki-shunsuke/github-test/pulls](https://github.com/hayasaki-shunsuke/github-test/pulls)
![image](https://user-images.githubusercontent.com/48468109/116080600-41abfc80-a6d4-11eb-8575-7b1d9663fb69.png)
![image](https://user-images.githubusercontent.com/48468109/116080618-47094700-a6d4-11eb-9c20-933207e8faba.png)
- [https://github.com/hayasaki-shunsuke/github-test/pulls](https://github.com/hayasaki-shunsuke/github-test/pulls)
![image](https://user-images.githubusercontent.com/48468109/116080659-4ffa1880-a6d4-11eb-93a6-cbd12f10eec1.png)
![image](https://user-images.githubusercontent.com/48468109/116080673-54263600-a6d4-11eb-81d0-f10afc87bb60.png)
## mainブランチにマージする
- レビューをしてもらい、`Merge pull request` を押す
![image](https://user-images.githubusercontent.com/48468109/116080686-59838080-a6d4-11eb-9e21-a364eccdec9f.png)
![image](https://user-images.githubusercontent.com/48468109/116080704-5f796180-a6d4-11eb-90cc-0992b8a507ea.png)
![image](https://user-images.githubusercontent.com/48468109/116080730-63a57f00-a6d4-11eb-8bd9-9916eb9be9a7.png)
- main ブランチに `[hayapi.md]` が追加されていることを確認
![image](https://user-images.githubusercontent.com/48468109/116080748-67d19c80-a6d4-11eb-83ae-6678e42ebee5.png)
