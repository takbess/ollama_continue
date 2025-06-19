
# Ollama + Continue

OllamaとContinueの設定・使い方に関するノート

## 環境構築方法
OllamaはWSL環境に、ContinueはWindows上のVS Codeにインストールすると簡単に構築できます。

### 1. Ollama のインストール
Ollamaをインストールするには、以下を実行します。
```bash
curl -fsSL https://ollama.com/install.sh | sh
# 動作確認
ollama run llama3
ollama run phi3
```

### 2. Continue のインストール
VS Codeの拡張機能検索から「Continue」をインストールします。  
その後、チャットやコーディングを実行するとモデルが自動的にインストールされます。


## モデルの変更方法
設定ファイル `C:\Users\{username}\.continue\config.json` を編集することでモデルを変更可能です。
自分の環境の例 [config.json](config.json)

例:
```json
"tabAutocompleteModel": {
    "title": "Qwen2.5-Coder 1.5B",
    "provider": "ollama",
    "model": "qwen2.5-coder:1.5b",
    // "apiBase": "https://your_ollama_server" ## コメントアウトすると、デフォルトでローカルのものが利用される
}
```
モデル名は [Continue Hub](https://hub.continue.dev/) で確認できます。
例えば、https://hub.continue.dev/ollama/qwen2.5-coder-1.5b?view=config


## モデルの比較
Continueで利用可能なモデルを以下のように比較しました。

| モデル名              | 特徴                                    | リソース要件                                | 最適な用途                                |
|-----------------------|-----------------------------------------|--------------------------------------------|-------------------------------------------|
| Llama 3.1:8b         | 汎用的で、コード補完・生成に適する      | GPU推奨 (例: RTX 3070), RAM 16GB以上       | 中規模プロジェクト、アイデア生成           |
| Starcoder2:3b        | コード生成に特化、小型で軽快            | GPU非搭載PCでも可 (処理速度低下あり)       | 軽量タスク、メモリ制限環境                 |
| DeepSeek-r1:8b       | 精密なコード生成、エラー検出に優れる    | GPU推奨、高メモリ環境                      | 高精度が必要な開発作業やデバッグ支援       |
| ELYZA-japanese-7b    | 日本語対応、UIデザインや文書生成向け    | GPU推奨, RAM 8GB以上                       | 日本語を用いた開発作業や文書生成           |


### 選び方のポイント
1. **VRAMに合わせて選択**
   - **4GB以下**: Starcoder2:3b  
   - **8GB程度**: DeepSeek-r1:8b / Llama3.1:8b  
   - **16GB以上**: Qwen2.5-Coder 32B  

2. **用途で選ぶ**
   - 軽量な補完タスク → Starcoder2  
   - 精密なコード生成 → DeepSeek / Qwen  
   - 日本語特化 → ELYZA  

3. **最新モデルをチェック**
   - DeepSeekやQwenが特化モデルの最新技術を備えています。
