# colcon コマンドのデフォルト設定

## 概要

- PythonでROSのパッケージを作成する場合，`colcon`コマンドで`build`を実行する際の`--symlink-install`オプションは，大変有力ですが，毎回指定するのは面倒です．
- コマンドラインで`--symlink-install`を指定せずに，このオプションを有効にする方法を紹介します．
- この本のDockerイメージでは，この方法を使っています．

## `--symlink-install`について

- `colcon build`を実行すると，パッケージのコマンドを実行するためのファイルが`src`ディレクトリから`install`ディレクトリへコピーされます．したがって，インタプリタ言語のPythonであっても，コードを書き換えて実行する度に`colcon build`の実行が必要です．
- `colcon build`を実行する際に，`--symlink-install`オプションを追加すると，コピーの代わりにシンボリックリンクが使われるので，コードを書き換えた後の`colcon build`の実行が不要になります．
- ただし，新しいファイルを追加した場合は，`colcon build`が必要です．
- また，`--symlink-install`オプションを付けたり付けなかったり混ぜて利用するとトラブルの元になりますので，統一するようにします．

## 設定方法

- ユーザの全てのcolcon buildの実行において`--symlink-install`オプションを有効にするには，そのユーザのホームディレクトリの下にディレクトリ`.colcon`を作り，その下に`defaults.yaml`という名前のファイルを作り，以下の内容を書きます．
```
{
    "build": {
        "symlink-install": true
    }
}
```

## この本のDockerイメージについて

- ユーザ`ubuntu`のホームディレクトリに`~/.colcon/defaults.yaml`を設定しています．
- Dockerイメージの中のビルド済みのこの本のROSパッケージは，`--symlink-install`でインストールされています．
- Dockerコンテナ内で新たに`colcon build`する場合もオプションを指定しなくても`--symlink-install`が有効になります．

## 参考文献

- [Configuration &mdash; colcon](https://colcon.readthedocs.io/en/released/user/configuration.html)