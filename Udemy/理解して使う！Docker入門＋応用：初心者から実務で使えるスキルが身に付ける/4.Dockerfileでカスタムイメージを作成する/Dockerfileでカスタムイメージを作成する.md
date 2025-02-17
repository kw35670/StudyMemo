# Dockerfileでカスタムイメージを作成する
## Dockerfileとは
自分でカスタムした、DockerImageを作成するための設計書のようなもの。  
DockerHubに存在するイメージの多くは、最低限の機能しか入っておらず、カスタマイズが必要。  
コンテナ内でBash等を使用して必要なソフトウェアをダウンロードしても、Imageからビルドしたら元に戻ってしまう。

## Dockerfileからイメージを作成する
```terminal
docker image build {ディレクトリパス}
```

## DockerImageに名前を付ける
```terminal
docker image build -t {任意のイメージ名}:{タグ名（任意）} {ディレクトリパス}
```

## RUNで任意のコマンドを実行
コマンド実行時に「y/n」のように選択を求められる場合、オプションで-yと付けておけば自動で選択してくれる。
```Dockerfile
FROM ubuntu:20.04

RUN apt update
RUN apt install -y curl
```

## COPYで任意にファイルをイメージに配置する
コピー先で指定したフォルダが存在しない場合は、新たに作成される。
```Dockerfile
COPY {コピー元} {コピー先}
```

## ビルドコンテキスト
ビルドコンテキストとDockerfileを別々で送る。
```terminal
docker image build -f docker/Dockerfile .
```

## .dockerignore
.dockerignoreを使用することで、ビルド時に送信したくないファイルを指定することが出来る。  
例：秘匿情報が入っているファイル。サイズが大きいファイル。
```.dockerignore
{送信したくないファイル名}
{送信したくないファイル名}
{送信したくないファイル名}
        .
        .
        .
```

## CMDでデフォルトコマンドを設定する
Dockerfileで一度しか使えない。  
複数のCMDがあれば、最後のCMDが優先される。

## RUNとCMDの違い
RUN： ビルド時に実行されるコマンド。  
CMD： コンテナ作成時に実行されるコマンド。

## ENVで環境変数を設定する
```terminal
ENV {key}={value} {key}={value} 
```
