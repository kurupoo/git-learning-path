# Git基礎学習完全ガイド
## 〜問題集形式で実践的にマスターする〜

### 🎯 学習概要

**学習方式**: 1問ずつの実践型問題集  
**学習時間**: 約1時間  
**達成レベル**: Git基礎操作の完全習得  
**実用度**: ⭐⭐⭐⭐⭐ 実際の開発で毎日使用するスキル

---

## 📚 学習内容（10問完全制覇）

### 🔰 初級レベル（第1-3問）
**基本操作とブランチ管理**

#### 第1問：リポジトリ状態確認
**問題文：** 現在のGitリポジトリの状態を確認してください。現在いるブランチ、ワーキングツリーの状態、コミット待ちのファイルがあるかどうかを調べるコマンドを実行してください。

**実行コマンド：**
```bash
git status
```

**期待される結果例：**
```
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

**習得スキル：** `git status` の完全理解

---

#### 第2問：ブランチ一覧表示
**問題文：** 現在のリポジトリにあるブランチの一覧を表示してください。ローカルブランチだけでなくリモートブランチも含めて表示してください。

**実行コマンド：**
```bash
git branch -a
```

**期待される結果例：**
```
* main
  test
  remotes/origin/main
  remotes/origin/test
```

**習得スキル：** `git branch -a` でローカル・リモート確認

---

#### 第3問：不要ブランチ削除
**問題文：** タイプミスしたブランチを削除してください。そのブランチに切り替わっていない状態で削除すること。

**実行コマンド：**
```bash
git branch -D [ブランチ名]
```

**期待される結果例：**
```
Deleted branch test-new-feauter (was 43ffde2).
```

**よくある間違い：**
- `-d` (小文字) vs `-D` (大文字) の使い分け
- 現在のブランチは削除できない

**習得スキル：** `git branch -D` で強制削除操作

---

### 🚀 中級レベル（第4-7問）
**ブランチ切り替えとファイル管理**

#### 第4-5問：ブランチ切り替えの体感
**問題文：** mainブランチからtestブランチに切り替えて、ファイル一覧を確認してください。その後mainブランチに戻って、ファイル構成の違いを確認してください。

**実行コマンド：**
```bash
git checkout test
ls
git checkout main
ls
```

**期待される結果：** ブランチごとにファイル構成が異なることを確認

**重要概念：** **ブランチ = 並行世界** の概念習得

---

#### 第6-7問：ファイル変更とステージング
**問題文：** testブランチでファイルを編集し、変更をGitで検出してからステージングエリアに追加してください。

**実行コマンド：**
```bash
git checkout test
vi test.yaml  # ファイル編集
git status    # 変更確認
git add test.yaml
git status    # ステージング確認
```

**期待される結果の変化：**
```
# 編集後
Changes not staged for commit:
        modified:   test.yaml

# add後
Changes to be committed:
        modified:   test.yaml
```

**習得概念：** Git 3段階管理の実践

---

### ⭐ 上級レベル（第8-10問）
**完全なGitワークフロー**

#### 第8問：コミット作成
**問題文：** ステージングされた変更をコミットしてください。

**実行コマンド：**
```bash
git commit -m "Update test.yaml with new configuration"
git status
```

**期待される結果：**
```
[test 2709c88] Update test.yaml with new configuration
 1 file changed, 1 insertion(+)
```

---

#### 第9問：GitHubへのpush
**問題文：** ローカルの変更をGitHubのtestブランチにpushして、その後の状態を確認してください。

**実行コマンド：**
```bash
git push
git status
```

**期待される結果：**
```
Writing objects: 100% (3/3), 293 bytes | 293.00 KiB/s, done.
To https://github.com/kurupoo/firstRepository.git
   43ffde2..2709c88  test -> test
```

**よくある間違い：**
- `origin` のスペルミス（`oring`, `orgin` など）
- upstream未設定エラー

---

#### 第10問：ブランチ間の独立性確認
**問題文：** mainブランチに切り替えて、testブランチとの違いを確認してください。

**実行コマンド：**
```bash
git checkout main
ls
git log --oneline -3
```

**期待される結果：** testブランチで追加したファイルがmainブランチには存在しないことを確認

**重要な理解：** ブランチの独立性の実体験

---

## 🏆 習得したスキル一覧

### ✅ 基本コマンド
- `git status` - 状態確認
- `git branch -a` - ブランチ一覧
- `git checkout` - ブランチ切り替え
- `git log --oneline` - 履歴確認

### ✅ 開発フローコマンド
- `git add` - ステージングエリアへ追加
- `git commit -m` - コミット作成
- `git push` - リモートリポジトリへ送信

### ✅ 重要概念の完全理解
- **ブランチの独立性**: 各ブランチが独自の「世界」を持つ
- **Git 3段階管理**: Working Directory → Staging Area → Repository
- **ローカル・リモート同期**: `ahead`/`up to date` の状態管理

---

## 💡 実践的な価値

### 🔥 実際の開発での活用例

```bash
# 新機能開発の典型的フロー
git checkout -b feature-login    # 新機能ブランチ作成
# ... コーディング作業 ...
git add .                        # 変更をステージング
git commit -m "Add login feature" # コミット
git push -u origin feature-login # GitHubにプッシュ
```

### 🛡️ 安全な開発環境
- **本番環境（main）を汚さない**: テストブランチで安全に実験
- **並行開発**: 複数機能を同時に開発可能
- **バックアップ**: 失敗してもいつでも安全な状態に復帰

---

## 📈 学習成果の証明

### Before（学習前）
```bash
git push
# → "Repository not found" エラー
# → SSH認証問題
# → Git概念が不明確
```

### After（学習後）
```bash
git status                    # 状態を正確に把握
git add test.yaml            # 適切にステージング
git commit -m "Update config" # 意味のあるコミット
git push                     # 成功！GitHubと完全同期
```

---

## 🚀 今後の学習ロードマップ

### 🎯 次のステップ
1. **中級編**: マージ操作、コンフリクト解決
2. **実践編**: プルリクエスト、コードレビュー
3. **チーム開発**: Git Flow、ブランチ戦略

### 💪 継続学習のポイント
- 毎日の開発でGitコマンドを意識的に使用
- 新しいプロジェクトでブランチ戦略を実践
- チームメンバーとのコラボレーション経験

---

## 🎊 まとめ

**問題集形式での学習効果**:
- ✅ 理論だけでなく実際のコマンド実行で体感的に習得
- ✅ 段階的レベルアップで無理なく上達
- ✅ 実際の開発フローを完全再現

**Git基礎スキル完全習得により、現代的な開発環境での作業が可能になりました！**

---

*Created by: 実践的Git学習プログラム*  
*Learning Method: 1問1答形式での段階的スキル習得*
