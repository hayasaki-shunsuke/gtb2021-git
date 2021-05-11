# practice(クリエイター向け)

## ブラウザからPull Requestを作成する
- 「hayasaki-shunsuke(自分のアカウント)/github-test」を作成する
- 「hayapi(自分のアカウント).md」を追加するPull Requestを作成する

# 手順
## github.com にアクセスしてブラウザからリポジトリを作成する
- 「hayasaki-shunsuke(自分のアカウント)/github-test」という名前のリポジトリ作成
    - [https://github.com/new](https://github.com/new)
    - `Add a README file` にチェック
    ![image](https://user-images.githubusercontent.com/48468109/116080303-da8e4800-a6d3-11eb-8bbd-2d44d4f32135.png)
    - [https://github.com/hayasaki-shunsuke/github-test](https://github.com/hayasaki-shunsuke/github-test)
    ![image](https://user-images.githubusercontent.com/48468109/116080360-ebd75480-a6d3-11eb-8907-4577bdaf7335.png)


## 新規ブランチを作成する
- https://github.com/hayasaki-shunsuke/github-test
- 「hayapi(自分のアカウント名)」ブランチを新規作成
![image](https://user-images.githubusercontent.com/48468109/117792978-bfe8d100-b286-11eb-96af-5ade5a08224d.png)

![image](https://user-images.githubusercontent.com/48468109/117793100-e0b12680-b286-11eb-93e3-741ae7fd27e5.png)

- https://github.com/hayasaki-shunsuke/github-test/tree/hayapi
![image](https://user-images.githubusercontent.com/48468109/117793178-f0306f80-b286-11eb-9adb-f8a8fa940d43.png)

## 追加するファイルを作成する
- `Add file` をクリック
- `Create new file` をクリック

![image](https://user-images.githubusercontent.com/48468109/117793494-3ede0980-b287-11eb-8e7c-0775367df5d2.png)

- ファイル名「hayapi(自分のアカウント名).md」を作成
- ファイルの中身を記入
```md
## hayapi
hayapiのテストファイルです。
```
- コメントを記入
```text
hayapi.md を新規作成
```
![image](https://user-images.githubusercontent.com/48468109/117794008-c4fa5000-b287-11eb-8801-b55069f3025f.png)

- `Commit new file`をクリック
- hayapi ブランチに「hayapi.md」が追加されたことを確認
![image](https://user-images.githubusercontent.com/48468109/117794316-173b7100-b288-11eb-8a45-9316c10d774f.png)

## Pull Requestを作成する
![image](https://user-images.githubusercontent.com/48468109/117794690-700b0980-b288-11eb-9588-bb82998a5e2e.png)
- 左上のメニューから `Pull requests` をクリック
    - https://github.com/hayasaki-shunsuke/github-test/pulls

- `Compare & pull request`をクリック

![image](https://user-images.githubusercontent.com/48468109/117794863-98930380-b288-11eb-86da-354a827693ed.png)

- https://github.com/hayasaki-shunsuke/github-test/compare/hayapi?expand=1
- Pull Request のタイトルとコメントを記述して`Create pull request` をクリックする

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
