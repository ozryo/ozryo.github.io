---
layout: post
title: "Octopressのめも"
date: 2014-04-01 16:29:20 +0900
comments: true
categories: 
---
技術の勉強で習得したことをアウトプットしたい人にとって、
ブログを活用するのはいいことと思えた。
<!--more-->
せっかくブログを始めるならばということで、GitPagesを利用しよう
GitPagesの利点
・GitHubに登録すれば始めれるので無料
・Git、Ruby、Octopress、Jekyllなどの技術に触れられる

まず、GitHubに登録を済まして、メールの認証をしておく。

てかGitPagesってなんなんだよ

　ウェブサイトをGitで管理して、GitHubへプッシュすることで公開される

　GitPagesにはユーザーサイトまたはオーガナイゼーションサイト、プロジェクトサイトがある。
　ユーザーサイトとオーガナイゼーションサイトはユーザー、オーガナイザに対して作ることができるGithubPagesであり、プロジェクトサイトはリポジトリに対して作成できる。
　プロジェクトサイトは、あるリポジトリにgh-pagesブランチを作成してそこに必要なファイルをPushすることにより公開できる。それ以外はmasterブランチが対象である。

　今回は、ユーザーサイトを作成するのでusername.github.ioリポジトリを作成して、静的ファイルをそこにPUSHすればOK

次にOctopressだ

自らhtmlファイルを作成して、pushしてなんて面倒くさすぎて論外。
そこでOctopressの出番である。

てかOctopressってなんなんだよ　簡単にいえば、Jekyllを使用してGithubPagesを作成するフレームワークなわけだから、Jekyllを理解する必要がある

で、Jekyllってなんなんだよ
　静的なブログを構築するためのRubyプログラム。ページや記事の原稿をファイルで管理してテンプレートエンジンであるLiquidを用いて原稿をテンプレートに埋め込んでいく
　フレームワークではなく、ファイルジェネレータ。Markdownやhtmlで書かれた原稿からブログに必要なhtml一式を出力する

　Jekyll は、予め想定された役割を持つファイル、ディレクトリで構成されている
##・_config.yml
YAML で記述したサイト構築用設定ファイルです。ここで設定した key: value は、グローバルな変数 site.key で参照できます。
##・_layouts/
ファイルに適用するテンプレートを置く場所です。テンプレートからは、Liquid タグ {{ content }} で、適用元のコンテンツが参照できます。
##・_includes/
汎用的もしくは部分的テンプレートを置く場所です。例えば _includes/file.ext は、Liquid タグ {% include file.ext %} で呼び出せます。
##・_posts/
ブログの原稿を置く場所です。予め、ファイル名の付け方とディレクトリの構造を _config.yml で permalink として定めておく必要があります。
##・_site/
最終的なサイトが出力される場所です。ここの内容をサーバーに転送するとサイトが出来上がります。
##・その他の特別なディレクトリ
特別な役割を持たせるディレクトリは、通例、先頭に _ を付け _config.yml に設定します。例えば Liquid 用のタグやフィルタの Ruby プログラムを置いておく _plugins があります。
##・その他のテキストファイル
上記以外に置かれたテキストファイルは、ファイル先頭のYAMLディレクティブで指定されたテンプレートに従ってレンダリングされ、テンプレートと同じファイル形式で_siteへ出力されます。YAMLのないファイルは、そのままスルーで出力されます。

ようやくOctopress
つまり、Jekyllを使用したフレームワークであると
作業環境にはRuby1.9.2以上が必要
とりあえず、インストールと初期設定に関しては、以下を参考にした。

http://qiita.com/syui/items/07365ed24eef63602233

では、実際に記事を投稿する手順は、

　・新規記事の作成
　　
　　rake new_post['title']
　　
　　この時点では、日本語をタイトルにできない。このコマンドによって作成されるsource/_posts/xxxxx.markdownをエディタで編集することにより、記事の内容、タイトルの変更ができる

　・記事の投稿（デプロイ）masterブランチにpushしている

　　rake gen_deploy
　　sourceブランチにもpushする
　　git add .
　　git commit -m 'message'
　　git push origin source
　　

　・記事のプレビュー（デプロイすると即公開なので）

　　rake generate
　　rake preview
　　http://localhost:4000にアクセス

