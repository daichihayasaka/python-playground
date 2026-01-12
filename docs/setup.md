# 環境構築

## UV

参考: [Working on projects](https://docs.astral.sh/uv/guides/projects/)

### プロジェクト作成

```bash
uv init python-playground
```

### コード実行

```bash
uv run main.py
```

#### 実行結果

venv が作成された

```bash
$ uv run main.py
Using CPython 3.13.3
Creating virtual environment at: .venv
Hello from python-playground!
```

### venv 有効化

```bash
source .venv/bin/activate
```

### パッケージインストール

#### 基本

```bash
uv add requests
```

#### development-dependencies

```bash
uv add --dev pytest
```

https://docs.astral.sh/uv/concepts/projects/dependencies/#development-dependencies

#### パッケージ情報確認

```bash
# バージョン確認
uv run pytest --version

# 詳細情報（依存関係含む）
uv pip show pytest

# インストール済みパッケージ一覧
uv pip list
```

#### パッケージ削除

```bash
uv remove requests
uv remove pytest --dev
```

#### 空の dependency-groups の削除

`uv remove` でグループ内の全パッケージを削除しても、空のグループは `pyproject.toml` と `uv.lock` に残る。

```toml
# こうなる
[dependency-groups]
dev = []
```

グループ自体を削除するコマンドは存在しないため、手動で `pyproject.toml` から削除し、`uv lock` を実行する。

```bash
# 1. pyproject.toml を編集して空の [dependency-groups] セクションを削除
# 2. lock ファイルを再生成
uv lock
```

**補足**

- 手動編集は公式にサポートされている: [Managing dependencies](https://docs.astral.sh/uv/concepts/projects/dependencies/)

  > "uv supports modifying the project's dependencies with uv add and uv remove, but dependency metadata can also be updated by editing the pyproject.toml directly"
  >
  > （uv は uv add と uv remove で依存関係を変更できるが、pyproject.toml を直接編集することもできる）

- 空グループの自動削除は未実装: [Issue #10956](https://github.com/astral-sh/uv/issues/10956)
  > "(nit: It would have been nice to have [dependency-groups] go away here.)"
  >
  > （空の dependency-groups が自動で消えてくれたら良かったのに）

## Ruff

### Tutorial

https://docs.astral.sh/ruff/tutorial/

#### Format

```bash
uv run ruff format --diff
uv run ruff format
```

#### Lint

```bash
uv run ruff check --diff
uv run ruff check --fix
```

### VSCode 拡張

https://github.com/astral-sh/ruff-vscode?tab=readme-ov-file#settings

## Docker

TBD
