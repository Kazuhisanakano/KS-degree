# KS-degree

## 使い方
VScodeで使用する場合"LaTeX Workshop"拡張機能をインストールし、後述の.vscode/setting.jsonを配置してください。
Overleaf等の環境では動作未確認です。latexmkrcにビルドレシピを記述してください。
本テンプレートのビルドレシピは以下のようにしています。
```
uplatex -> upbibtex -> uplatex -> uplatex -> dvipdfmx
```

## 引用スタイル
IEEEスタイル？のような？フォーマットです。main.tex内で"\bibliographystyle{unsrtnat}"としています。
Master-paper.bibのauthorフィールドにおいて、姓名の間にスペースを入れるとエラーが起きます。注意してください。

## ファイル構成
```
.
├── main.tex
├── title.tex
├── abstract.tex
├── Master-paper.bib
├── latexmkrc
├── chapter/
│   ├── chapter1.tex
│   ├── chapter2.tex
│   └── ...
├── appendix/
│   └── appendix.tex
├── image/
│   ├── image1.png
│   └── ...
└── .vscode/
    └── settings.json
```
### 本文関連
- ./main.tex : title.tex, abstract.tex, chapterX.texを集約するファイルです。ビルドの際に指定してください。
- ./title.tex : 表紙を記述します。
- ./abstract.tex : アブストラクトを記述します。
- ./chapter : 各"chapterX.tex"に章を分けて記述します。
- ./image : 論文内で使用する図を格納します。
- ./Master-paper.bib : 引用文献を記述します。
- ./appendix : 付録を記述します。

### ビルドファイル
VScodeを使用する場合は.vscode/settings.jsonを配置します。
VScode以外ではlatexmkrcを使用します。(動作未確認)

以下にsettings.jsonの動作確認済みの例を示します。設定ファイルのため、リポジトリには含めていません。
```json:settings.json
{
    "workbench.startupEditor": "none",
    "workbench.colorTheme": "Monokai Dimmed",
    "emmet.triggerExpansionOnTab": true,
    "editor.cursorSmoothCaretAnimation": "on",
    "workbench.list.smoothScrolling": true,
    "editor.smoothScrolling": true,
    "terminal.integrated.smoothScrolling": true,
    "jupyter.askForKernelRestart": false,
    "[python]": {
        "editor.formatOnType": true
    },
    "code-runner.runInTerminal": true,
    "window.zoomLevel": -1,
    "git.openRepositoryInParentFolders": "never",
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOC%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "lualatex",
            "command": "lualatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "uplatex",
            "command": "uplatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "%DOC%"
            ]
        },
        {
            "name": "upbibtex",
            "command": "upbibtex",
            "args": [
              "%DOCFILE%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        },
        {
            "name": "dvipdfmx",
            "command": "dvipdfmx",
            "args": [
                "-o",
                "%DOC%.pdf",
                "%DOC%.dvi"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "日本語論文ビルド",
            "tools": [
                "uplatex",
                "upbibtex",
                "uplatex",
                "uplatex",
                "dvipdfmx"
            ]
        },
        {
            "name": "latexmk (pdf)",
            "tools": ["latexmk"]
        },
        {
            "name": "pdflatex ➞ bibtex ➞ pdflatex × 2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        },
        {
            "name": "xelatex",
            "tools": ["xelatex"]
        },
        {
            "name": "lualatex",
            "tools": ["lualatex"]
        },
        
        {
            "name": "uplatex ➞ dvipdfmx",
            "tools": [
                "uplatex",
                "dvipdfmx"
            ]
        }
    ],
    "latex-workshop.latex.recipe.default": "日本語論文ビルド",
    "latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.latex.autoBuild.run": "onFileChange",
    "latex-workshop.latex.clean.enabled": true,
    "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.brf",
        "*.idx",
        "*.ilg",
        "*.ind",
        "*.lof",
        "*.log",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.fdb_latexmk",
        "*.synctex.gz"
    ],
    "latex-workshop.synctex.afterBuild.enabled": true,
    "latex-workshop.message.update.show": false,
    "editor.wordWrap": "on",
    "files.autoSave": "onFocusChange"
}
```


