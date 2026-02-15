# CLAUDE.md

このファイルは、このリポジトリでコードを扱う際に Claude Code (claude.ai/code) に対する指針を提供します。

## 全体的な指針

- 指示に対して Claude は日本語で回答してください。

## コマンド

### 開発

- `npm run dev` - 開発サーバーを起動（作業ディレクトリ: NKNS/）
- `npm run build` - 本番用にビルド（作業ディレクトリ: NKNS/）
- `npm run preview` - 本番ビルドをプレビュー（作業ディレクトリ: NKNS/）
- `npm run lint` - コード品質チェックのため ESLint を実行（作業ディレクトリ: NKNS/）

### 重要なビルドノート

- ビルド出力では、public/のファイルが/dist 直下に一列で配置される（フラット化構造）
- public ファイルパスが変更された場合、プロジェクト内の VBA マクロも調整が必要
- JSON ファイルは正常に動作するために UTF-8 エンコードである必要がある

## アーキテクチャ

これは日本の建設会社のウェブサイト向けの React TypeScript アプリケーションです。メインコードは `NKNS/` ディレクトリに配置されています。

### アプリケーション構造

- **React Router DOM v6**を使用した Single Page Application
- 再利用可能なモーダルと UI コンポーネントを持つ**コンポーネントベースアーキテクチャ**
- React ステートを使用した**クライアントサイドデータ管理**（バックエンドなし）
- `/public/project.json`に保存された**プロジェクトデータ**（UTF-16 エンコード、特別な TextDecoder が必要）

### 主要ページ

- **HomePage**: 会社のヒーローセクションを含むランディングページ
- **AboutPage**: 会社情報と履歴
- **PolicyPage**: 企業方針とスタッフプロフィール
- **ProjectsPage**: フィルタリングと管理 CRUD 機能を持つメインプロジェクトショーケース

### コアコンポーネント

- **Navbar/Footer**: レスポンシブデザインのレイアウトコンポーネント
- **ProjectModal**: 画像カルーセル付きプロジェクト詳細ビューア
- **AdminModal**: プロジェクト管理インターフェース（作成・編集・削除）

### 技術スタック

- React 18 + TypeScript
- Vite ビルドツール
- カスタムネイビー/オレンジブランディングの TailwindCSS
- Lucide React アイコン
- React Router DOM v6

### データ管理

- `/public/project.json`に保存されたプロジェクト構造:
  ```typescript
  interface Project {
    id: number;
    title: string;
    category: string; // residential, commercial, public, industrial
    location: string;
    year: string;
    description: string;
    images: string[]; // /public/画像への相対パス
  }
  ```
- useState/useEffect を使用して React コンポーネントで全状態を管理
- 外部データベースや API 呼び出しなし

### スタイリングとローカライゼーション

- UI テキストとコンテンツ全体で日本語を使用
- 建設業界向けのプロフェッショナルデザイン
- モバイル対応レイアウト
- ブランドカラー用のカスタム TailwindCSS 設定
