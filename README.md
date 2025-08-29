# `@hidekitux/biome-config`

neostandardと主要なESLintプラグインから移植したBiome v2設定集です。

## 📦 インストール

```bash
bun add -D @biomejs/biome @hidekitux/biome-config
# または
npm install --save-dev @biomejs/biome @hidekitux/biome-config
```

## 🚀 使い方

### 標準設定

`biome.json`:
```json
{
  "extends": ["@hidekitux/biome-config/standard"]
}
```

### 標準設定 + React/JSX/CSS

`biome.json`:
```json
{
  "extends": [
    "@hidekitux/biome-config/standard",
    "@hidekitux/biome-config/react"
  ]
}
```

### 標準設定 + テスト

`biome.json`:
```json
{
  "extends": [
    "@hidekitux/biome-config/standard", 
    "@hidekitux/biome-config/test"
  ]
}
```

## 📋 設定ファイル

### `biome.standard.json` - ベース設定
汎用的なJavaScript/TypeScript向け設定。以下のESLintプラグインのルールを移植：

- ✅ neostandard
- ✅ eslint-plugin-unicorn
- ✅ eslint-plugin-unused-imports
- ✅ typescript-eslint
- ✅ eslint-plugin-regexp
- ✅ eslint-plugin-no-secrets
- ✅ eslint-plugin-n (Node.js)
- ✅ eslint-plugin-import-access
- ✅ eslint-plugin-import

**主な特徴:**
- インデント: スペース2つ
- セミコロン: 必要な場合のみ
- クォート: シングルクォート
- 末尾カンマ: なし
- 認知的複雑度の制限
- TypeScript型の厳密なチェック
- インポート/エクスポートの最適化
- Node.jsグローバル変数のサポート

### `biome.react.json` - React/JSX/CSS設定
`biome.standard.json`を継承し、React/JSX/CSS向けの設定を追加：

- ✅ React Hooks検証
- ✅ JSXフォーマット
- ✅ CSS/Sass/Less/CSS Modulesサポート
- ✅ アクセシビリティ（a11y）ルール
- ✅ Next.js対応
- ✅ Storybook対応

**追加機能:**
- JSX属性: ダブルクォート
- React Hooks依存関係の検証
- CSSプロパティ検証
- セマンティックHTML推奨
- コンポーネントファイル名規則

### `biome.test.json` - テスト設定
`biome.standard.json`を継承し、テスト環境向けの設定を追加：

- ✅ Jest/Vitest/Cypress/Mocha対応
- ✅ テスト用グローバル変数
- ✅ テスト特有のルール緩和
- ✅ モック/フィクスチャ対応
- ✅ E2E/統合テスト対応

**主な特徴:**
- テストフレームワークのグローバル変数（describe, it, expect等）
- 複雑度制限の緩和（20まで許可）
- console使用許可
- フォーカステスト検出（エラー）
- スキップテスト検出（警告）
- テストファイルからのエクスポート禁止
