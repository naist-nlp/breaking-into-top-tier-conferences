# Breaking into Top-Tier Conferences

https://naist-nlp.github.io/breaking-into-top-tier-conferences/

このレポジトリは言語処理学会第32回年次大会（NLP2026）併設ワークショップ「気軽に国際会議を目指しましょう」のHPのために整備されました。しかしながら、今後のワークショップ開催などのために、公開手順などを、備忘録も兼ねてこのREADMEに記述します。できる限りハンズオン形式で進めます。

制作者: yusuke1997



## 1. GitHub Pagesでサイトを公開するまでの手順

ここでは、シンプルだけど、ACL併設ワークショップなどで実際に使われているようなHPを、**最小限の努力で作成する方法**を紹介します。凝った話や細かいテクニックなどについては専門家や詳しい人に聞いて下さい。すべてmainブランチで作業することを念頭に置いています。

### 1.1 GitHub PagesのURLを取得する

新しくレポジトリを作成してください。このとき、
https://github.com/naist-nlp/breaking-into-top-tier-conferences
が
https://naist-nlp.github.io/breaking-into-top-tier-conferences/
のように、レポジトリ名が直接URLになります。あとで変更可能ですので、とりあえず名付けましょう。

 例外的に`naist-nlp.github.io` のように`{ユーザ名}.github.io` というレポジトリを作った場合のみ、該当のURLになります。またカスタムURLを持っている人は何でもいいので、とりあえずレポジトリ作ればあとでそのURLに変更できます。レポジトリ作成時はChoose visibilityはPublicで公開お願いします。Add READMEをOnにしてREADME.mdも空でいいので作成してください。忘れたらあとで適当に作成してください。

その後、Settings -> Pagesとボタン見つけて、GitHub Pagesの設定画面まで飛んでください。パッと見つからなければ、command + FでSettingsやPagesを検索して、ボタンを見つけてください。

Build and deploymentで、`Deploy from a branch` 、Branchを `main /(root)` にしておきましょう。そしてsaveボタン押せば、公開されると思うので、https://github.com/naist-nlp/breaking-into-top-tier-conferences のようにURLにアクセスしてみましょう。だめだった時やボタンとかがうまく見つからない時は、Build and deployment画面を何回かリロードして同じこと試してみましょう。

SettingsやCodeなどのタブ欄にActionsというタブがあるので、それを押して最新の `pages build and deployment` を押してみて、無事deployにチェックがついていればOKです。更新に時間がかかっている場合は、茶色いマークが出ます。commit番号の隣とか、色んなところで出ます。失敗の場合は赤いバツマークが出るので、気長に待ちましょう。ずっと茶色ならリロード、時々HPもリロードして公開されているか確認。

また、ドメインをやっぱ変更したいってときは、Pagesの欄にカスタムURLがあるので、独自に変更するか、レポジトリの名前を変更すればすぐ変更できます。これは以降のどの段階でも可能です。

### 1.2 Jekyllでモダンなテーマに設定

いまの状態だと、URLにアクセスしても、404エラーのページが表示されるだけだと思います。
そのため、とりあえず一旦、編集可能な状態をめざしましょう。
といっても簡単で「設定ファイル(`_config.yml`)」と「本文(`index.md`)」のたった2つのファイルを作るだけで完成します。

はじめに、`index.md` というファイルをREADME.mdなどと同じルートとなる階層で作成してください。
`# 気軽に国際会議を目指しましょう`
とこの段階では書き込みましょうか。
後々の編集ではindex.mdをmarkdownのように編集することで、勝手にhtmlの形式に変換してくれます。

次に、`_config.yml` というファイルを同様に作成し、

```yaml
title: "Breaking into Top-tier Conferences"
description: "気軽に国際会議を目指しましょう"
theme: jekyll-theme-minimal
```

などのように記述してください。titleは文字通りタイトル、descriptionは簡単な説明です。HP公開時に直感的にこれらがどのように機能しているかわかるので、適当でも良いです。

ここで一番のポイントとなるのは、themeのところです。`jekyll-theme-minimal` とりあえず、設定していますが、基本的にGitHub Pagesでサポートされている13 (14?) 種類のテンプレートであれば、なんでも良いです。
https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll#supported-themes

基本的に`jekyll-theme-{テーマ名}`で簡単に切り替えることができます。
`jekyll-remote-theme` というのも使えますが、段々個別事例になってくるので、ChatGPTとかに聞いて下さい。

最後にcssの設定です。このままでも公開できますが、ただのhtml直書きファイルになるので、お化粧しましょう。
`/assets/css/style.scss` というファイルを作って、

```css
---
---

@import "{{ site.theme }}";
```

と書き込むだけです。上の`---`なども忘れないようにしましょう。丸コピでいいです。これで指定したthemeのcssを自動で使うことができます。

現状をまとめると

```bash
.
├── _config.yml
├── assets
│   └── css
│       └── style.scss
├── index.md
└── README.md
```

のようになっていると思います。この状態でgit pushしましょう。そうしたら更新が行われて1,2分のうちにサイトに変化があるはずです。

今回はthemeを`jekyll-theme-minimal`にしました。例えば、BlackboxNLP（2024年まで）やNegative Result NLPなどで使われています。これらのGitHubなどを参考にカスタマイズしてください。

- https://insights-workshop.github.io/index
- https://blackboxnlp.github.io/2024/

また、`jekyll-theme-cayman`だとACL系のSRWで採用されています。
https://acl2025-srw.github.io/

`_config.yaml` などの書き方はこれらのレポジトリを見るのが手っ取り早いので、参考にしてください。あと、必ず公式のドキュメントとかを確認するようにしましょう。最悪わからなければ、ChatGPTやGeminiにまずは5分程度聞いてみて、解決を試みてください。

- https://github.com/acl2025-srw/acl2025-srw.github.io/blob/main/_config.yml
- https://github.com/insights-workshop/insights-workshop.github.io/blob/master/_config.yml

### 1.3 ローカル環境で試す

上記の手順で公開されたサイトをindex.mdを編集することで、どんどん更新することができます。最小限は整いましたが、何度もコミットして確認するのは手間ですし、コミットやActionsの履歴が汚くなりがちです。そのため、手元のパソコン（MacBook）で確認できるようにしましょう。

まずは環境のセットアップから。homebrewが入っている前提で話を進めます。

```bash
export HOMEBREW_NO_AUTO_UPDATE=1 # auto-updateが走って本題ではないパッケージのupdateで時間消耗を防ぐ
brew install ruby
# ここは色々変化するので、直前のbrew install ruby終了後に出てくるpathに指定にしてください。
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH' >> ~/.zshrc 
brew install nodebrew
nodebrew setup
# ここも色々変化するので、直前のnodebrew setup終了後に出てくるpathに指定にしてください。
echo 'export PATH=/opt/homebrew/var/nodebrew/current/bin:$PATH' >> ~/.zshrc 
source ~/.zshrc
nodebrew install stable
ruby -v; node -v; npm -v
# ruby 3.4.1
# v24.11.1
# 11.6.4
```

ここまでで、実行環境の手前まで揃いました。次に、`Gemfile`という拡張子なしのファイルをREADME.mdなどと同様にルートに作成し、以下のように記述して保存します。

```
source 'https://rubygems.org'

gem "github-pages",
group: :jekyll_plugins
```

そのあと、`bundle install` とコマンドを打つと、`Gemfile.lock`というファイルが出てきているはずです。
最後に `bundle exec jekyll serve` と入力すると、実行されるので表示に従って `http://127.0.0.1:4000`などと入力すれば、ローカル環境で再現できていると思います。

もしどこかで引っかかったら、ログを一個ずつ辿ってください。例えばこのドキュメント執筆中、rubyのversionが2.6と低くてbundle installが実行できませんでした。このように、大抵はメジャーバージョン違いによるものです。また、基本的に実行時のterminalの表示に色々書いているので、焦らずによく読んでみてください。わからないなら実行画面のコピペして、ChatGPTなどに聞いてみてください。これ系のエラー対応は生成AIの得意分野なので楽をしましょう。
また、なにか変になったらとりあえずリロードとか、実行中止からもう一度起動するなど、初歩的な解決法でうまくいくはずです。

そろそろ、`.gitignore`でいらないファイルを設定しておくほうが良いです。

```
.DS_Store
*~
*.lock
vendor
_site
```





### 参考文献

- https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll
- https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll
- https://qiita.com/naoko_s/items/4b02dd07ed3bf191efd3
- https://zenn.dev/ykmkn/articles/c0888431d39bcc
- https://github.com/orgs/pages-themes/repositories?type=all
- https://attonblog.blogspot.com/2018/05/disable-homebrew-auto-update.html
- https://qiita.com/naoki-atjp/items/f27b8e7c10e6c793055c
- 

---

## 2. ワークショップのHPっぽい内容にする

1章で土台を作りました。ここでは、ワークショップの内容を充実させましょう。
論文投稿などを受け付ける場合、call for paper (cfp) などの作成が必要になってきますが、とりあえずここでは一旦なにも考えずに、とりあえず、サイト公開時に最低限の情報が載っているようにしたいです。

TODO: あとでcfp1のときのindex.mdのリンクを貼り付ける。
https://github.com/naist-nlp/breaking-into-top-tier-conferences/blob/72ebe7c085efa8b48f7d86cf7518daef96edb3bc/index.md


### 2.1 ロゴを作成する

ロゴはChaGPTに生成してもらいましょう。理由としてGeminiだと長方形になるので、ChatGPTの正方形が良いです。以下のようなプロンプトで良いです。あとはいい感じに調理してくれます。使ったら謝辞にも使ったことを明記しておきましょう。

「気軽に国際会議を目指しましょう（Breaking into Top-Tier Conferences）というワークショップにぴったりなロゴを生成して」

作成したロゴを`assets/img` の中に格納しましょう。

```
assets
├── css
│   └── style.scss
└── img
    ├── logo.png
    ├── title_logo_sketch.png
    └── title_logo.png
```

そのあと、`config.yml` に `logo: assets/img/logo.png` という一行を追加してください。そのあと、リロードや再起動とかすれば、ロゴが表示されているはずです。

また、`index.md` に `![気軽に国際会議を目指しましょう](assets/img/title_logo.png "title_logo")`のように一行差し込めば、狙った位置に画像が表示されます。

画像が重くなりがちなので、適宜圧縮とかしてください。

### 2.2 レイアウトを変えてみる

そろそろデフォルトのレイアウトが窮屈になってきた頃だと思います。編集方法は簡単で、使用しているテンプレートのもとサイトここでは [minimal](https://github.com/pages-themes/minimal/blob/master/_layouts/default.html) の`_layouts/default.html` をコピペして、おなじように自分が作成しているサイトの`_layouts/default.html`に貼り付けてください。

これでレイアウト情報を自分たちで編集できるようになります。例えば、logoとtitleの順序を入れ替えてみるなど、フレキシブルにできるし、Insight NLPではページリンクを付けて、目次のようにしていたりします。参考文献にあるような実装を参考に、編集してみてください。

### 参考文献

- https://gist.github.com/Tatzyr/3847141
- https://github.com/insights-workshop/insights-workshop.github.io/blob/master/_config.yml
- https://github.com/blackboxnlp/2024/blob/main/_config.yml







