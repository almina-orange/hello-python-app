# hello-ruby-app

## Info
* Heroku Simple Tutorial
* 超初歩的な Heroku x ruby

## Basic Component
```
.
|-- .gitignore
|-- .python-version     # python バージョン管理ファイル
|-- Procfile            # heroku app 処理管理ファイル
|-- app.json            # heroku app パッケージ管理ファイル
|-- requirements.txt    # pip バージョン管理ファイル
|-- venv                # python 仮想環境
|   |-- bin
|   |   `-- ...
|   |-- include
|   |   `-- ...
|   |-- lib
|   |   `-- ...
|   |-- pip-selfcheck.json
|   `-- pyvenv.cfg
|-- hello.py            # main script
`-- README.md           # this
```

## How to startup?
1. `venv`でディレクトリに仮想環境を構築

    ```sh
    $ python -m venv [$DIR_NAME]
    $ source [$DIR_NAME]/bin/active  # 仮想環境の起動
    ```

2. 必要パッケージのインストール

    ```sh
    $ pip install 'requests[security]'  # SSL通信用パッケージ
    $ pip install flask  # python 用webアプリケーションフレームワーク
    $ pip install gunicorn  # WSGIサーバ（アプリケーションとwebサーバの接続用）
    ```

3. `requirements.txt`への出力

    ```sh
    $ pip freeze > requirements.txt
    ```

4. `Procfile`の作成

    ```
    web: gunicorn hello:app --log-file=-
    ```

5. `hello.py`を作成，リクエストに "Hello World" で応答

    ```python
    from flask import Flask

    app = Flask(__name__)

    @app.route('/')
    def hello():
        return 'Hello World'
    ```

6.  `.gitignore`を作成，`venv/`を追加

    ```sh
    $ echo "venv/" > .gitignore
    ```

7.  git リポジトリと heroku app を作成，リモートに push する

    ```sh
    $ git init
    $ git add . && git commit -m "[$MESSAGE]"
    $ heroku app create [$APP_NAME]
    $ git push heroku master
    ```

8.  `curl`および`heroku open`で heroku app を確認

    ```sh
    $ curl https://[$APP_NAME].herokuapp.com
    $ heroku open
    ```

Note
* `venv`と`pyenv`の併用
    * `venv`は 3.3 以降のみなので注意
    * `pyenv`で指定バージョンの python に切り替え

        ```sh
        $ pyenv install *.*.*
        $ pyenv local *.*.*
        ```

    * `venv`で仮想環境を構築

        ```sh
        $ python -m venv [$DIR_NAME]
        $ source [$DIR_NAME]/bin/activate
        ```


------

## Ref
* Python アプリをクラウドにデプロイ・運用・スケール - Heroku, [https://jp.heroku.com/python](https://jp.heroku.com/python)