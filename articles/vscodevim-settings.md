---
title: "いろいろ考えた末のVScodeVimの設定"
emoji: "👻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Vim, 環境構築, VSCode]
published: true
---

# はじめに

この設定は mattun さんの記事を参考にしました。ほとんどそのままですが、私の使用しているキーボードは英語配列なので少し変更しています。

https://qiita.com/koutarn/items/06d34c279ca06c977884

# キーボードについて

使用しているキーボードが英語配列で、Ctrl+Space を日本語入力への切り替えに使用しているので、Ctrl+Space のキーバインドは使用しない。

## settings.json

```json
{
  // visual studio codeの設定

  //========================================================================
  // vscodeのeditorの設定
  //========================================================================
  "editor.fontSize": 16, //fontsize
  "editor.wordWrap": "on", //1行長くならないように
  "editor.lineHeight": 0, //1行の高さ
  "editor.renderLineHighlight": "all", //現在の行番号含めて強調表示する
  //   "editor.minimap.enabled": false, //minimap削除
  "editor.insertSpaces": true, //tabをスペースとして扱う
  //   "editor.tabSize": 4, //tabをデフォルトで4にする
  "editor.renderWhitespace": "boundary", //エディタ上での空白表示設定
  "editor.renderControlCharacters": true, //制御文字の表示
  "editor.cursorBlinking": "smooth", //カーソルの点滅をヌルヌルにする
  "editor.autoIndent": "full", //autoindentを入れる
  "editor.fontFamily": "Cica, Consolas, 'Courier New', monospace", //font settings
  "extensions.autoUpdate": true, //プラグインを自動アップデート
  "editor.autoClosingBrackets": "beforeWhitespace",
  "editor.autoClosingQuotes": "beforeWhitespace",
  "breadcrumbs.enabled": false, //パンクズリストはそんなに使わないし非表示
  "editor.detectIndentation": false,
  "git.enableSmartCommit": true,

  //サジェスチョン
  "editor.quickSuggestionsDelay": 400, //入力補完の検出タイミング

  // "editor.quickSuggestions":false,
  "editor.quickSuggestions": {
    //入力補完を自動で表示する
    "other": true, //文字列以外
    "strings": false, //文字列
    "comments": false //コメント
  },

  "editor.tokenColorCustomizations": {
    "comments": {
      "foreground": "#7f9ea0", //コメントの色
      "fontStyle": ""
    },

    "functions": {
      "fontStyle": "underline"
    }
  },

  //encodings

  // 有効な場合、ファイルを開くときに文字セット エンコードを推測します。言語ごとに構成することも可能
  "files.autoGuessEncoding": true,

  "files.autoSave": "off", //ダーティファイルの作成を無効化
  "files.eol": "auto", //既定の改行文字をautoにする

  "[typescript]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "diffEditor.ignoreTrimWhitespace": false,
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },

  "[scss]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
  },

  // ワークベンチ設定
  "workbench.editor.showTabs": true, // タブを表示
  "workbench.editor.enablePreview": false, //毎回新規で開く
  "workbench.editor.enablePreviewFromQuickOpen": false, //毎回新規で開く
  "workbench.colorCustomizations": {
    "editor.lineHighlightBackground": "#002255", //現在の行の背景色
    "editor.selectionBackground": "#31ca4a77", //選択業の背景
    "editor.selectionHighlightBorder": "#00e1ff", //線学業の前背景
    "editorError.border": "#ff0000", //エラーの下線の色
    "tab.activeBorder": "#ffffff", //アクティブなタブの色
    "tab.inactiveForeground": "#999999", //アクティブでないタブの色
    "editorSuggestWidget.selectedBackground": "#4792b4", //選択しているサジェストの背景色
    "editorSuggestWidget.foreground": "#f1efef", //選択しているサジェストの文字色
    "editorWhitespace.foreground": "#8a8888" //tab等の制御文字
  },
  //nnoremap
  "vim.normalModeKeyBindingsNonRecursive": [
    { "before": ["J"], "after": ["1", "0", "j"] }, //移動を早める
    { "before": ["K"], "after": ["1", "0", "k"] }, //移動を早める
    { "before": ["H"], "after": ["0"] }, //端に移動
    { "before": ["L"], "after": ["$"] }, //端に移動
    { "before": ["<Leader>", "h"], "after": ["<C-w>", "h"] }, //window移動
    { "before": ["<Leader>", "j"], "after": ["<C-w>", "j"] }, //window移動
    { "before": ["<Leader>", "k"], "after": ["<C-w>", "k"] }, //window移動
    { "before": ["<Leader>", "l"], "after": ["<C-w>", "l"] }, //window移動
    {
      "before": ["]"],
      "commands": [{ "command": "C_Cpp.PeekDeclaration" }],
      "when": ["editorLangId == c"]
    }, //宣言を見る c専用
    {
      "before": ["["],
      "commands": [{ "command": "editor.action.peekDefinition" }]
    }, //定義を見る
    { "before": ["<Leader>", "s"], "commands": [":split"] }, //水平に開く
    { "before": ["<Leader>", "v"], "commands": [":vsplit"] }, //水平にを閉じる
    { "before": [">"], "commands": ["editor.action.indentLines"] }, //インデント調整(repeat可能)
    { "before": ["<"], "commands": ["editor.action.outdentLines"] }, //インデント調整(repeat可能)
    { "before": ["<Leader>", "u"], "after": ["g", "t"] }, //tab移動
    { "before": ["<Leader>", "y"], "after": ["g", "T"] }, //tab移動
    { "before": ["<Leader>", "x"], "commands": [":q!"] }, //tabを閉じる
    { "before": ["<Leader>", "q"], "commands": [":qa!"] }, //すべてを閉じる
    { "before": ["<Leader>", "w"], "commands": [":wa"] }, //すべてを保存
    { "before": ["<Leader>", "o"], "after": ["o", "<ESC>"] }, //空の行を挿入
    { "before": ["<Leader>", "O"], "after": ["O", "<ESC>"] }, //空の行を挿入
    {
      "before": ["<Leader>", "c"],
      "commands": [{ "command": "editor.action.commentLine" }]
    },
    //コメント
    {
      "before": ["<Leader>", ":"],
      "commands": [{ "command": "workbench.action.showCommands" }]
    },
    //コマンドパレット
    {
      "before": ["<Leader>", ";"],
      "commands": [{ "command": "workbench.action.quickOpen" }]
    },
    //ファイル検索
    { "before": ["<CR>"], "after": ["G"] }, //最終行へ
    { "before": ["<BS>"], "after": ["g", "g"] }, //先頭行へ
    // 検索結果を画面中央に
    { "before": ["n"], "after": ["n", "z", "z"] },
    { "before": ["N"], "after": ["N", "z", "z"] },
    { "before": ["*"], "after": ["*", "z", "z"] },
    { "before": ["#"], "after": ["#", "z", "z"] },

    //Surround
    { "before": ["s"], "after": ["y", "s"] }, //surround add

    //easy motion
    { "before": ["f"], "after": ["<Leader>", "<Leader>", "2", "s"] }, //easymotion 2s

    //Multi-Cursor Mode
    //prefix Ctrl
    { "before": ["<C-n>"], "after": ["g", "b"] }, //選択した文字に対して増やす
    {
      "before": ["<C-k>"],
      "commands": [{ "command": "editor.action.insertCursorAbove" }]
    },
    {
      "before": ["<C-j>"],
      "commands": [{ "command": "editor.action.insertCursorBelow" }]
    },

    //外部プラグイン呼び出し
    // {
    //   "before": ["<Leader>", "@"],
    //   "commands": [
    //     { "command": "markdown-preview-enhanced.openPreviewToTheSide" }
    //   ]
    // } //markdownで開く
    {
      "before": ["u"],
      "commands": ["undo"]
    },
    {
      "before": ["<C-r>"],
      "commands": ["redo"]
    },
    {
      "before": ["leader", "d"],
      "commands": ["editor.action.revealDefinition"]
    }
  ],
  "vim.insertModeKeyBindings": [
    {
      "before": ["j", "j"],
      "after": ["<Esc>"]
    },
    { "before": [";", ";"], "commands": ["editor.action.triggerSuggest"] }
  ],
  "vim.visualModeKeyBindingsNonRecursive": [
    //vを押した直後はvのコマンドが残っているので注意
    //visualmode後にすぐ実行したいものは、二重で定義する。
    { "before": ["J"], "after": ["1", "0", "j"] }, //移動を早める
    { "before": ["v", "J"], "after": ["1", "0", "j"] }, //移動を早める
    { "before": ["K"], "after": ["1", "0", "k"] }, //移動を早める
    { "before": ["v", "K"], "after": ["1", "0", "k"] }, //移動を早める
    { "before": ["v"], "after": ["a", "f"] }, //拡大選択
    { "before": ["v", "v"], "after": ["a", "f"] }, //拡大選択
    { "before": ["H"], "after": ["0"] }, //端に移動
    { "before": ["L"], "after": ["$", "h"] }, //端に移動
    { "before": ["v", "H"], "after": ["0"] }, //端に移動
    { "before": ["v", "L"], "after": ["$", "h"] }, //端に移動
    { "before": [">"], "commands": ["editor.action.indentLines"] }, //インデント調整(repeat可能)
    { "before": ["<"], "commands": ["editor.action.outdentLines"] }, //インデント調整(repeat可能)
    {
      "before": ["<Leader>", ":"],
      "commands": [{ "command": "workbench.action.showCommands" }]
    }, //コマンドパレット
    {
      "before": ["<Leader>", ";"],
      "commands": [{ "command": "workbench.action.quickOpen" }]
    }, //ファイル検索
    {
      "before": ["<Leader>", "c"],
      "commands": [{ "command": "editor.action.commentLine" }]
    }, //コメント

    //Multi-Cursor Mode

    //選択した文字に対して増やす
    { "before": ["<C-n>"], "after": ["g", "b"] },

    //行末尾にカーソルを出す
    {
      "before": ["<C-l>"],
      "commands": [
        { "command": "editor.action.insertCursorAtEndOfEachLineSelected" }
      ]
    },

    //外部プラグイン呼び出し
    {
      "before": ["<Leader>", "b"],
      "commands": [{ "command": "alignment.align" }]
    }, //揃える
    {
      "before": ["<Leader>", "v"],
      "commands": [{ "command": "extension.commentaligner" }]
    } //コメントを揃える
  ],

  "workbench.colorTheme": "One Dark Pro",
  "javascript.updateImportsOnFileMove.enabled": "always", //surroundを有効にする

  //========================================================================
  //plugin settings
  //========================================================================

  //========================================================================
  //VIM
  //========================================================================
  "vim.statusBarColorControl": false, //statusbarの色のコントロールをしない
  "vim.highlightedyank.enable": true, //yankした箇所をハイライト表示にする
  "vim.highlightedyank.color": "rgba(0, 240, 170, 0.5)", //yankした時の色
  "vim.highlightedyank.duration": 150, //yankした時の色の表示時間
  "vim.leader": "<space>", //Map Leaderの設定
  "vim.autoindent": true, //autoindent
  "vim.useSystemClipboard": true, //system clipboardと同期する
  "vim.hlsearch": true, //hlserch
  "vim.visualstar": true, //カーソル上にあるワードを"*"で検索
  "vim.useCtrlKeys": true, //諸々のctrlキーを使った操作が有効になる
  "vim.debug.silent": true, //アラートを出さない
  "vim.timeout": 1200, //入力のタイムアウト時間

  // vim plugin有効化
  "vim.easymotion": true, //easy motionを有効化
  "vim.surround": true, //surroundを有効にする

  //easy motion
  "vim.easymotionMarkerForegroundColorOneChar": "rgba(0,240,170,0.9)", //一文字目の色
  "vim.easymotionMarkerForegroundColorTwoChar": "rgba(0,240,170,0.9)", //二文字目の色
  "vim.easymotionMarkerBackgroundColor": "", //背景色
  "vim.easymotionMarkerWidthPerChar": 19, //各文字に割り当てられている幅
  "vim.easymotionMarkerHeight": 0, //マーカーの高さ
  "vim.easymotionMarkerFontFamily": "Cica", //フォント
  "vim.easymotionMarkerFontSize": "12.5", //フォントサイズ
  "vim.easymotionMarkerFontWeight": "normal", //フォントの太さ
  "vim.easymotionKeys": "asdfhjklwqeruioopghty;", //マーカーに使用される文字列
  "vim.easymotionMarkerYOffset": 13.5, //高さのずれ修正

  // zenhan
  "vim.autoSwitchInputMethod.enable": true,
  "vim.autoSwitchInputMethod.defaultIM": "0",
  "vim.autoSwitchInputMethod.obtainIMCmd": "D:\\zenhan\\bin64\\zenhan.exe 0",
  "vim.autoSwitchInputMethod.switchIMCmd": "D:\\zenhan\\bin64\\zenhan.exe {im}"
}
```

## keybindings.json

```json
// 既定値を上書きするには、このファイル内にキー バインドを挿入しますauto[]
[
  // サジェスチョン操作
  {
    "key": "ctrl+j",
    "command": "selectNextSuggestion",
    "when": "suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus"
  },
  {
    "key": "ctrl+k",
    "command": "selectPrevSuggestion",
    "when": "suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus"
  },

  //コマンドパレットの移動
  {
    "key": "ctrl+j",
    "command": "workbench.action.quickOpenSelectNext",
    "when": "inQuickOpen"
  },
  {
    "key": "ctrl+k",
    "command": "workbench.action.quickOpenSelectPrevious",
    "when": "inQuickOpen "
  },

  //editorじゃない時の操作(editorではvscodevimのコマンドが有効になる)
  //tabを閉じる
  {
    "key": "space x",
    "command": "workbench.action.closeActiveEditor",
    "when": "!editorTextFocus && !editorHasSelection && !editorHasMultipleSelections && !inQuickOpen && !sideBarFocus && !panelFocus"
  },
  //tabを進める
  {
    "key": "space u",
    "command": "workbench.action.nextEditor",
    "when": "!editorTextFocus && !editorHasSelection && !editorHasMultipleSelections && !inQuickOpen && !sideBarFocus && !panelFocus"
  },
  //tabを戻す
  {
    "key": "space y",
    "command": "workbench.action.previousEditor",
    "when": "!editorTextFocus && !editorHasSelection && !editorHasMultipleSelections && !inQuickOpen && !sideBarFocus && !panelFocus"
  },
  //markdownのpreviewから戻る
  {
    "key": "space h",
    "command": "workbench.action.focusPreviousGroup",
    "when": "!editorTextFocus && !editorHasSelection && !editorHasMultipleSelections && !inQuickOpen && !sideBarFocus && !panelFocus"
  },
  //コマンドパレットを開く
  {
    "key": "space oem_1",
    "command": "workbench.action.showCommands",
    "when": "!editorTextFocus && !editorHasSelection && !editorHasMultipleSelections && !inQuickOpen && !sideBarFocus && !panelFocus"
  },
  //ファイルを開く
  {
    "key": "space oem_plus",
    "command": "workbench.action.quickOpen",
    "when": "!editorTextFocus && !editorHasSelection && !editorHasMultipleSelections && !inQuickOpen && !sideBarFocus && !panelFocus"
  },

  /* -------------------------------------------------------------------------- */
  /*                                  sidebar                                   */
  /* -------------------------------------------------------------------------- */

  //サイドバー表示(toggle)
  {
    "key": "shift+space shift+space",
    "command": "workbench.action.focusFirstEditorGroup"
    // "command": "workbench.action.toggleSidebarVisibility",
    // "when": "!explorerViewletVisible && !searchViewletVisible && !inDebugMode && vim.mode != 'SearchInProgressMode' && vim.mode != 'Insert'"
  },
  {
    "key": "shift+space shift+space",
    "command": "workbench.action.toggleSidebarVisibility",
    "when": "explorerViewletVisible && !searchViewletVisible && !inDebugMode && vim.mode != 'SearchInProgressMode' && vim.mode != 'Insert'"
  },

  // サイドバーからの移動
  {
    "key": "shift+space l",
    "command": "workbench.action.focusFirstEditorGroup"
    // "when": "explorerViewletVisible && explorerViewletFocus && !editorFocus && !inQuickOpen"
  },

  /* -------------------------------- explorer -------------------------------- */
  //explorer表示
  {
    "key": "shift+space shift+e",
    "command": "workbench.view.explorer"
  },
  {
    "key": "shift+space e",
    "command": "workbench.view.explorer"
  },
  //エクスプローラー間移動
  {
    "key": "j",
    "command": "list.focusDown",
    "when": "explorerViewletFocus && explorerViewletVisible && !inputFocus"
  },
  {
    "key": "k",
    "command": "list.focusUp",
    "when": "explorerViewletFocus && explorerViewletVisible && !inputFocus"
  },

  //新規ファイル作成
  {
    "key": "n",
    "command": "explorer.newFile",
    "when": "explorerViewletFocus && explorerViewletVisible && !inputFocus"
  },
  //新規フォルダ作成
  {
    "key": "f",
    "command": "explorer.newFolder",
    "when": "explorerViewletFocus && explorerViewletVisible && !inputFocus"
  },

  //エクスプローラーでフォルダを開く
  {
    "key": "e",
    "command": "revealFileInOS",
    "when": "explorerViewletFocus && explorerViewletVisible && !inputFocus"
  },

  //リネーム
  {
    "key": "r",
    "command": "renameFile",
    "when": "explorerViewletFocus && explorerViewletVisible && !inputFocus"
  },
  //削除
  {
    "key": "d",
    "command": "deleteFile",
    "when": "explorerViewletFocus && explorerViewletVisible && !inputFocus"
  },

  // //svn操作
  // {
  //     "key": "s",
  //     "command": "tortoise-svn ...",
  //     "when": "explorerViewletFocus && explorerViewletVisible && !inputFocus",
  //     "args":"explorerPath",
  // },

  /* ----------------------------- grep検索(sidebar) ---------------------------- */
  {
    "key": "shift+space shift+f",
    "command": "workbench.action.findInFiles",
    "when": "!searchInputBoxFocus"
  },

  // 検索ボックスへ移動
  {
    "key": "shift+space f",
    "command": "workbench.action.findInFiles",
    "when": "!searchInputBoxFocus"
  },

  /* ---------------------------- debug(sidebar) ---------------------------- */
  {
    "key": "shift+space ctrl+d",
    "command": "workbench.view.debug"
  },

  {
    "key": "shift+space d",
    "command": "workbench.view.debug"
  },

  /* -------------------------- version管理(sidebar) -------------------------- */

  {
    "key": "shift+space shift+s",
    "command": "workbench.view.scm"
  },
  {
    "key": "shift+space s",
    "command": "workbench.view.scm"
  },

  /* --------------------------- plugin管理(sidebar) -------------------------- */

  {
    "key": "shift+space shift+z",
    "command": "workbench.view.extensions"
  },
  {
    "key": "shift+space z",
    "command": "workbench.view.extensions"
  },

  /* -------------------------------------------------------------------------- */
  /*                                    Panel                                   */
  /* -------------------------------------------------------------------------- */

  //パネルから戻る
  {
    "key": "shift+space k",
    "command": "workbench.action.focusLastEditorGroup",
    "when": "panelFocus && !editorTextFocus && !editorHasSelection && !editorHasMultipleSelections && !inQuickOpen"
  },

  // //パネルを出す
  // {
  //   "key": "ctrl+space ctrl+p",
  //   "command": "workbench.action.togglePanel",
  //   "when": "vim.mode != 'SearchInProgressMode' && vim.mode != 'Insert'"
  // },

  /* ---------------------------- terminal(panel) --------------------------- */
  {
    "key": "shift+space shift+t",
    "command": "workbench.action.terminal.toggleTerminal",
    "when": "vim.mode != 'SearchInProgressMode' && vim.mode != 'Insert'"
  },
  {
    "key": "shift+space t",
    "command": "workbench.action.terminal.toggleTerminal",
    "when": "vim.mode != 'SearchInProgressMode' && vim.mode != 'Insert'"
  },

  /* ---------------------------- error画面(panel) ---------------------------- */
  {
    "key": "shift+space shift+q",
    "command": "workbench.actions.view.problems"
  },
  {
    "key": "shift+space q",
    "command": "workbench.actions.view.problems"
  }
]
```

## 補足

フォントには Cica を使用しています。
https://github.com/miiton/Cica

インサートモードからノーマルモードへ戻るとき、自動的に英字入力モードへ戻るようにするために、zenhan を使用しています。
https://qiita.com/iuchi/items/9ddcfb48063fc5ab626c
