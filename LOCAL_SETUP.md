# ローカルでJekyllを動かす手順

## 1. Rubyをインストールする

### Windows

RubyInstaller を使うのが簡単です。

1. RubyInstaller for Windows をインストール
2. インストール時に MSYS2 / DevKit も入れる
3. PowerShell または コマンドプロンプトで確認

```bash
ruby -v
gem -v
```

### macOS

Homebrew と rbenv を使って、安定版のRuby 3.1 系をインストールします。
（※最新の Ruby 3.2 以上を入れると Jekyll 3.x の依存ライブラリでエラーが出るため）

```bash
# 1. rbenv と ruby-build をインストール
brew install rbenv ruby-build

# 2. PATH の設定（初回のみ）
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(rbenv init - zsh)"' >> ~/.zshrc
source ~/.zshrc

# 3. Ruby 3.1.4 をインストールして標準に設定
rbenv install 3.1.4
rbenv global 3.1.4

# 4. バージョン確認 (ruby 3.1.4... と出ればOK)
ruby -v
```

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install ruby-full build-essential zlib1g-dev
ruby -v
```

## 2. Bundlerを入れる

```bash
gem install bundler
```

## 3. このプロジェクトへ移動

```bash
cd uehara-lab
```

## 4. 依存関係を入れる

```bash
bundle install
```

## 5. ローカルサーバを起動

```bash
bundle exec jekyll serve --livereload
```

ブラウザで開きます。

```text
http://127.0.0.1:4000/
```

## 6. よくあるエラー

### `webrick` がないと言われる

Ruby 3.x 系で出ることがあります。この一式では `Gemfile` に `webrick` を入れています。まだエラーが出る場合は次を実行してください。

```bash
bundle add webrick
bundle install
```

### 日本語ファイルや文字化けが気になる

ファイルは UTF-8 で保存してください。

### GitHub Pages のURLで CSS やリンクが崩れる

プロジェクトページで公開する場合、`_config.yml` の `baseurl` をリポジトリ名に変更してください。

例：

```yaml
baseurl: "/uehara-lab"
```

ユーザーサイト `https://USERNAME.github.io/` で公開する場合は空のままで大丈夫です。

```yaml
baseurl: ""
```

## 7. ビルドだけ確認したい場合

```bash
bundle exec jekyll build
```

生成物は `_site/` に出力されます。
