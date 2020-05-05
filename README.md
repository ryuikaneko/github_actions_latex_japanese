# GitHub Actionsで英語or日本語のTeXのコンパイル

* やりたいこと
  * GitHub Actionsを使って「pushしたらTeXがコンパイルされて、最終的にどこかへpdfがアップロードされる」システムがほしい。
  * 英語にも、日本語にも対応してほしい。
  * できれば、人の褌で相撲を取りたい。

* やったこと
  * 既にパッケージ[latex-action](https://github.com/marketplace/actions/latex-compilation)があったので利用させてもらった。
  * 英語のTeXファイルは./test/につっこんだ。
  * 日本語のTeXファイルは./test_jp/につっこんだ。
  * 英語版については./.github/workflows/test.ymlに[latex-action](https://github.com/marketplace/actions/latex-compilation)のexampleを記入した。デフォルトではlatexmkを使用している。
  * 日本語版については.latexmkrcでplatexやdvipdfmx等を使うように設定した。.latexmkrcは./test_jp/につっこんだ。（通常はlatexmkを実行した場所にある.latexmkrcが、自動的に読み込まれるため。）test.ymlの引数はargsで設定でき、dvi経由でpdf作成するように"args: -pdfdvi"とした。
  * pdfの場所については、ActionsのArtifactsにzipファイルがアップロードされるようにした。（例えば[ここ](https://github.com/ryuikaneko/github_actions_latex_japanese/actions/runs/95157463)。）test.ymlの"uses: actions/upload-artifact@master"の箇所が、この指定方法に対応する。なお、タグ付け等の凝ったことはしていない。
  * 今の例だと、pushしてから約3分ほどでpdfの入ったzipがアップロードされた。

* 参考文献
  * 今回利用させてもらった本家
    * https://github.com/xu-cheng/latex-action
    * https://github.com/dante-ev/latex-action
  * 同様のシステムを日本語で構築しているもの
    * https://qiita.com/takuseno/items/2b4c4a129205d03526ad
    * https://github.com/takeru1205/latex_build
    * https://github.com/denkiuo604/tex-to-pdf
    * https://qiita.com/denkiuo604/items/63b8c34a60a2340727b1
    * https://qiita.com/denkiuo604/items/137a1b3fc1955cfb9c58
    * https://qiita.com/denkiuo604/items/c33088b1ab542f354d22

----

* 追記（2020/05/05）
  * ReVTEXに日本語コメントを入れる例を追加した（ファイルは./revtex/、実行結果は[ここ](https://github.com/ryuikaneko/github_actions_latex_japanese/actions/runs/95953146)）。
  * 名前に日本語、中国語（繁体字・簡体字）、韓国語も挿入してみた。
  * ファイルの文字コードはUTF-8。
