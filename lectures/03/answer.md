# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：今回の比較では素のLLMを実行していないため未比較。
- `--trace` で見えたツール呼び出し（ツール名と引数）：変更前は `search_glossary({'query': 'LoRA'})` と `search_glossary({'query': 'QLoRA'})` の2回。docstring 変更後は `search_glossary({'query': 'LoRA QLoRA'})` の1回。
- 1つの質問での LLM 呼び出し回数（`requests`）：変更前・変更後とも2回。ツール呼び出し数（`tool_calls`）は2回から1回に変化。
- 追加したツールと、docstring に書いた説明：ツールの追加はなし。既存の `search_glossary` の説明を、検索語を1つだけ入れる内容から、複数の用語をまとめて入れる内容に変更。

## 宿題

- 取り組んだレベル：基礎
- やったこと：モデル `gemini-3.5-flash-lite` に同じ質問「LoRAとQLoRAの違いは？」を `--trace` 付きで実行し、変更前と docstring 変更後を比較した。
- 結果：変更前は用語ごとに `search_glossary` を呼び、引数は `LoRA` と `QLoRA`、`tool_calls=2` だった。変更後は引数を `LoRA QLoRA` にまとめ、`tool_calls=1` になった。どちらも `requests=2`。回答はいずれもLoRAとQLoRAの違いを説明し、第2回に関連づけていた。表現や箇条書きの形式には違いがあった。
- 気づき・疑問：ツールの docstring はモデルがツールをどう使うかに影響し、複数の用語をまとめて検索することでツール呼び出し数が減った。`[tool return]` は先頭120文字までの表示なので、返却内容の全体はtraceだけでは確認できない。
