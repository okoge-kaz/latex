# How to Set up Latex Environment on macOS

1. Install mactex

   `brew install --cask mactex-no-gui `

2. update TexLive

   `sudo tlmgr update --self --all`

   If you don't use sudo, you will get some errors.

3. create .latexmkrc

   `touch ~/.latexmkrc`

   and add the following lines to it

   ```
   #最大のタイプセット回数
   $max_repeat = 5;
   #DVI経由でPDFをビルドすることを明示
   $pdf_mode = 3;

   #pLaTeXを使う
   #-halt-on-error:初めのエラーで終わらせる
   $latex = 'platex %O %S -halt-on-error';

   #pBibTeXを使う(参考文献)
   $bibtex = 'pbibtex %O %S';

   #Mendexを使う(索引)
   $makeindex = 'mendex %O -o %D %S';

   #DVIからPDFへの変換
   $dvipdf = 'dvipdfmx %O -o %D %S';
   ```

4. add the following lines to your vscode settings.json

   ```json
     <!-- latex settings -->
     <!-- viewerをタブで開く -->
     "latex-workshop.view.pdf.viewer": "tab",
     <!-- intellisenseを有効にする -->
     "latex-workshop.intellisense.package.enabled": true,
     <!-- 生成ファイルを格納するディレクトリ名 -->
     "latex-workshop.latex.outDir": "latex_out",
     <!-- 自動でPDFを更新 -->
     "latex-workshop.latex.autoBuild.run": "onFileChange",
     <!-- 生成ファイルで削除するファイル -->
     "latex-workshop.latex.autoClean.run": "onBuilt",
     "latex-workshop.latex.clean.fileTypes": [
       "*.aux",
       "*.bbl",
       "*.blg",
       "*.dvi",
       "*.fdb_latexmk",
       "*.fls",
       "*.synctex.gz",
       "*.toc"
     ],
     <!-- ビルドの動作 -->
     "latex-workshop.latex.recipes": [
       {
         "name": "latexmk",
         "tools": ["latexmk"]
       }
     ],
     <!-- ビルドのコマンド -->
     "latex-workshop.latex.tools": [
       {
         "name": "latexmk",
         "command": "latexmk",
         "args": ["-outdir=%OUTDIR%", "%DOC%.tex"]
       }
     ],
     "latex-workshop.bibtex-format.sort.enabled": true,
     "workbench.editorAssociations": {
       "*.pdf": "latex-workshop-pdf-hook"
     }
   ```

5. install dependencies for using latexindex

   `brew install perl`

   `brew install cpanm`

   `cpanm Log::Log4perl Log::Dispatch::File YAML::Tiny File::HomeDir Unicode::GCString`

All done! Now you can use latex in vscode.

## Install jlisting

Cloud Latex と同様の環境をつくるために、試行錯誤した記録

1. `kpsewhich listings.sty`

   で、listings.sty のパスを調べる

2. cd でそのパスに移動

3. open . でそのパスを Finder で開く

4. [listings.sty](./jlisting.sty)を追加

5. `sudo mktexlsr`

## References

- https://zenn.dev/ganariya/articles/vscode-latex-indent
- https://qiita.com/DaikiSuyama/items/d463c5b7afdabc5fcde5
- https://qiita.com/N_Matsukiyo/items/1199f07a0e1bf4fce29c
