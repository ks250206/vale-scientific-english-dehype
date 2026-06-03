# Vale style: Scientific English De-Hype

`scientific-english-dehype` は、科学論文の英語から過度に宣伝的な表現、根拠よりも印象で押す表現、LLM らしい定型句を検出するための Vale スタイルです。

このリポジトリには、ローカルで使うための Vale 設定、GitHub Actions で pull request をチェックするワークフロー、確認用の例文、手動レビュー用チェックリストが含まれています。文章を自動で書き換えるのではなく、「ここは根拠に対して表現が強すぎないか」を確認するための lint として使います。

## できること

- `novel`, `remarkable`, `robust`, `significant` など、根拠確認が必要な強い形容詞を検出する
- `delve into`, `pivotal`, `intricate`, `showcasing`, `leverage` など、AI で磨いた文章に見えやすい語を検出する
- `demonstrates`, `proves`, `confirms`, `reveals` など、主張の強さを上げる動詞を検出する
- `drives`, `prevents`, `leads to`, `results in` など、因果を示す表現を検出する
- abstract で具体的な結果の代わりに promotional なまとめだけになっている箇所を見つける
- `write-good`, `proselint`, `Readability`, `Google`, `Microsoft`, `alex` の汎用スタイルで、冗長表現、読みやすさ、技術文書寄りの用語、inclusive language も併せて確認する
- Markdown、LaTeX、plain text の原稿に対してローカルと CI の両方でチェックする

## ファイル構成

```text
.vale.ini
.github/styles/ScientificEnglishDehype/*.yml
.github/styles/ScientificEnglishDehype/README.md
.github/workflows/vale.yml
docs/CHECKLIST.md
examples/bad.md
examples/good.md
```

主な役割は次の通りです。

- `.vale.ini`: Vale の対象ファイル、使用スタイル、TeX コマンドや数式などの無視設定
- `.github/styles/ScientificEnglishDehype/*.yml`: 実際の検出ルール
- `.github/workflows/vale.yml`: GitHub Actions 用の Vale 実行設定
- `docs/CHECKLIST.md`: Vale の検出後に人間が確認するためのチェックリスト
- `examples/bad.md`: 検出される表現の例
- `examples/good.md`: より具体的で控えめな表現の例

## インストール

Vale をインストールします。macOS では Homebrew が簡単です。

```bash
brew install vale
```

インストール確認:

```bash
vale --version
```

この設定では Vale の公開パッケージも使うため、初回と `.vale.ini` の `Packages` を変更した後にパッケージを同期します。

```bash
vale sync
```

このリポジトリを別の論文リポジトリで使う場合は、次のファイルとディレクトリを論文リポジトリのルートへコピーします。

```bash
cp .vale.ini /path/to/manuscript-repo/
cp -R .github/styles /path/to/manuscript-repo/.github/
cp .github/workflows/vale.yml /path/to/manuscript-repo/.github/workflows/
cp docs/CHECKLIST.md /path/to/manuscript-repo/docs/
```

## ローカルでの基本的な使い方

まず付属の悪い例で動作を確認します。

```bash
vale examples/bad.md
```

良い例も確認できます。

```bash
vale examples/good.md
```

実際の原稿を確認する場合:

```bash
vale manuscript.md
vale manuscript.tex
vale manuscript.txt
```

複数ファイルをまとめて確認する場合:

```bash
vale abstract.md introduction.md discussion.md
vale sections/*.md
vale manuscript/*.tex
```

この設定では `.vale.ini` により、次の拡張子が対象です。

```text
*.md
*.txt
*.tex
```

## LaTeX 原稿を lint する

LaTeX 原稿は plain text として Vale に渡します。`.vale.ini` では、一般的な TeX コマンド、数式、URL、図表番号、コードブロック、`equation` や `figure` などの環境をできるだけ無視するようにしています。

```bash
vale manuscript.tex
```

出力が多すぎる場合は、本文セクションだけを対象にします。

```bash
vale sections/abstract.tex
vale sections/introduction.tex
vale sections/discussion.tex
```

または、本文だけを Markdown や text に書き出して確認します。

```bash
pandoc manuscript.tex -t markdown -o build/manuscript.md
vale build/manuscript.md
```

## docx 原稿を lint する

Vale は `.docx` を直接 lint するための設定にはしていません。Word 原稿を確認する場合は、いったん Markdown または text に変換してから Vale を実行します。

Pandoc を使う例:

```bash
mkdir -p build/vale
pandoc manuscript.docx -t markdown -o build/vale/manuscript.md
vale build/vale/manuscript.md
```

一時ファイルを残さずに、Pandoc の出力をそのまま Vale に渡すこともできます。標準入力にはファイル拡張子がないため、`--ext='.md'` で Markdown として扱わせます。

```bash
pandoc manuscript.docx -t markdown | vale --ext='.md'
```

macOS の `textutil` を使って text に変換する例:

```bash
mkdir -p build/vale
textutil -convert txt manuscript.docx -output build/vale/manuscript.txt
vale build/vale/manuscript.txt
```

Word から手動で書き出した text ファイルを確認する例:

```bash
vale manuscript-exported.txt
```

変換後のファイルは一時ファイルとして扱い、必要に応じて `build/` や `tmp/` に置くと、原稿本体と lint 用の派生物を分けて管理できます。

## 出力の読み方

Vale の出力には、ファイル名、行番号、ルール名、メッセージが表示されます。

例:

```text
examples/bad.md:3:12:ScientificEnglishDehype.HypeWords
Check whether 'remarkable' is supported by concrete evidence.
```

この場合は、`remarkable` が常に禁止という意味ではありません。近くに数値、比較、実験条件、検証結果などがあり、その語が本当に必要かを確認します。情報が増えない形容詞であれば削除し、情報が必要なら測定値や比較に置き換えます。

## レビューの進め方

推奨フローは次の通りです。

1. `vale` を実行する
2. 検出箇所を機械的に削るのではなく、`docs/CHECKLIST.md` を見ながら根拠と表現の強さを確認する
3. 強すぎる表現を、測定値、比較対象、手法、実験条件、再現性、統計情報に置き換える
4. 書き換え後にもう一度 `vale` を実行する
5. 残す表現については、本文中のデータで支えられているかを確認する

特に abstract では、次のような書き換えを優先します。

```text
Before: This study provides valuable insights into robust ion transport.
After: The measured ionic conductivity was X S cm-1 at Y degC, compared with Z S cm-1 for the reference sample.
```

## CI での使い方

このリポジトリの `.github/workflows/vale.yml` は、GitHub Actions で Vale を実行します。対象は pull request と `main` への push です。

チェック対象のパス:

```text
**/*.md
**/*.tex
**/*.txt
.vale.ini
.github/styles/**
```

GitHub Actions では `vale-cli/vale-action@v2.1.2` を使い、Vale `3.10.0` を実行します。pull request では GitHub の check として結果が表示されます。

このスタイルのルールは、多くが `warning` または `suggestion` です。`novel`、`robust`、`significant` のような語は文脈によって正当化できるため、初期状態では「確認すべき箇所」として扱います。

CI を失敗させたいルールは、該当する `.yml` の `level` を `error` に変更します。

```yaml
level: error
```

ワークフロー側では `fail_on_error: true` が設定されているため、`error` が出ると CI が失敗します。

## 追加した汎用スタイル

このスタイルは論文向けの独自ルールに加えて、Vale の汎用パッケージも有効にしています。論文ではすべてを機械的に直すのではなく、検出結果を確認候補として扱ってください。

| パッケージ | 論文での使いどころ | 注意 |
| --- | --- | --- |
| `write-good` | 冗長表現、weasel words、cliché、受動態などの確認 | 受動態は Methods などで自然な場合があり、論文ではうるさすぎることがあります |
| `proselint` | 一般的な英語スタイルの臭い検出 | 論文特有ではないため、専門用語や定型表現でノイズが出ることがあります |
| `Readability` | 文の長さ、読みやすさ指標の確認 | 数式、化学式、長い化合物名、引用が多い箇所ではノイズが出ます |
| `Google` | 明快な技術文書寄りの表現の確認 | 論文よりドキュメント向けのため、投稿規定や分野の文体を優先してください |
| `Microsoft` | 用語、表記、文体の一貫性の確認 | 製品ドキュメント寄りの指摘も含まれます |
| `alex` | inclusive language の確認 | 論文、申請書、共同研究資料では有用な場合があります |

有効化しているパッケージは `.vale.ini` の `Packages` と `BasedOnStyles` にあります。検出が多すぎる場合は、まず `MinAlertLevel` を `warning` に上げるか、`BasedOnStyles` から一時的に対象パッケージを外して、独自ルールと汎用ルールを分けて確認します。

## docx を CI で確認したい場合

`.docx` を CI で確認したい場合も、直接 Vale に渡すのではなく、CI 上で Markdown または text に変換してから lint します。例えば Pandoc を使う場合は、ワークフローに変換ステップを追加します。

```yaml
- name: Install Pandoc
  run: sudo apt-get update && sudo apt-get install -y pandoc

- name: Convert docx manuscripts
  run: |
    mkdir -p build/vale
    find . -name '*.docx' -not -path './build/*' -print0 \
      | xargs -0 -I{} sh -c 'pandoc "$1" -t markdown -o "build/vale/$(basename "$1" .docx).md"' sh {}

- name: Run Vale on converted docx
  run: vale build/vale/*.md
```

既存の `vale-action` と併用する場合は、通常の Markdown/LaTeX/text は `vale-action` に任せ、docx 由来の変換ファイルだけを追加ステップで確認すると運用しやすくなります。

## ルールの調整

ルールは `.github/styles/ScientificEnglishDehype/*.yml` にあります。

検出が多すぎる場合:

```yaml
level: suggestion
```

厳しくしたい場合:

```yaml
level: error
```

特定の語をプロジェクトで許容したい場合は、該当ルールから語を外すか、より具体的な正規表現に変更します。化学式、引用、TeX コマンド、URL などのノイズは `.vale.ini` の `TokenIgnores` と `BlockIgnores` で調整します。

## よくある運用

原稿全体を確認:

```bash
vale manuscript.md
```

abstract だけを重点確認:

```bash
vale abstract.md
```

Word 原稿を変換して確認:

```bash
pandoc manuscript.docx -t markdown -o build/vale/manuscript.md
vale build/vale/manuscript.md
```

修正後に全体を再確認:

```bash
vale examples/*.md docs/*.md manuscript.md
```

ルールファイルも含めてリポジトリ内の対象ファイルを確認:

```bash
vale .
```

## 注意点

- Vale は根拠の有無を完全には判定できません。検出結果は「確認候補」です。
- `significant` は統計的有意性を意味する場合があります。その場合は、p 値、信頼区間、検定方法などが近くにあるかを確認します。
- `.tex` は完全な LaTeX パーサーとして処理されるわけではありません。ノイズが多い場合は本文だけを変換して確認してください。
- `.docx` は Markdown または text に変換してから確認してください。
- すべての警告を消すことより、主張の強さとデータの強さを合わせることを優先してください。

## License

MIT ks250206 2026
