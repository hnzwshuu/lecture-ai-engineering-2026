# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前：`app.agent` は `search_glossary`、`get_lecture_summary`、`make_quiz`、`search_materials` の4個。MCP エージェントは `glossary_search_glossary`、`glossary_get_lecture_summary`、`glossary_make_quiz` の3個。
- STEP 2 の [tool call]：[tool call]   glossary_search_glossary({'query': '3レベル'})
- STEP 3 の [tool call]：[tool call]   fetch_fetch({'url': 'https://modelcontextprotocol.io/'})
- STEP 4 の [tool call]：
  - [tool call]   aws_aws___search_documentation({'search_phrase': 'Amazon S3 バージョニング 概要', 'topics': ['general']})
  - [tool call]   aws_aws___search_documentation({'topics': ['general'], 'search_phrase': 'Versioning S3 what is it'})
- 気づき・疑問：質問に応じて `glossary_search_glossary` が `3レベル` を検索し、用語集の定義をもとに「基礎・実装・発展」の3段階を説明した。STEP 3 では、`uvx` で起動した fetch サーバーの `fetch_fetch` が URL を取得し、MCP の概要を日本語で要約した。STEP 4 では、URL で接続した AWS の MCP サーバーが検索語を変えて2回 `aws_aws___search_documentation` を呼び出し、S3 のバージョニングについて、過去のバージョンを保持して誤操作による上書き・削除からデータを保護できると説明した。設定には `command` を使うとサーバーを自分の環境で起動でき、`url` を使うと外部で動くサーバーに接続できる。外部サーバーでは、渡した情報が提供者に送られる可能性があるため、提供元とリスクを確認する必要がある。

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：`app/mcp_server.py` を確認し、`server.tool()(tools.get_lecture_summary)` がすでに登録されていたため、追加の変更は行わなかった。エージェント側の設定・コードも変更せず、ツール一覧と「第2回では何を学びますか？」への応答、テストを確認した。
- 結果：ツール一覧に `glossary_get_lecture_summary` が表示され、質問時に `glossary_get_lecture_summary({'lecture': 2})` が呼び出された。`uv run pytest -q` は23件すべて成功した。
- 気づき・疑問：MCP エージェントは起動時にサーバーからツール一覧を取得するため、サーバー側でツールが公開されていれば、エージェント側のコードを変更しなくても利用できることを確認した。今回は登録済みだったため、ファイルの変更は発生しなかった。
