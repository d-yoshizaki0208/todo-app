# ToDoリスト MVP基本設計書

## 1. 技術スタック

- **フロントエンド**: React 18.x
- **言語**: TypeScript 5.x
- **スタイリング**: Tailwind CSS 3.x
- **状態管理**: React Hooks (useState, useEffect)
- **ビルドツール**: Vite
- **パッケージマネージャー**: npm または yarn

## 2. プロジェクト構成

```
todo-app/
├── public/
│   └── favicon.ico
├── src/
│   ├── components/
│   │   ├── Header/
│   │   ├── TodoForm/
│   │   ├── TodoList/
│   │   ├── TodoItem/
│   │   └── Footer/
│   ├── types/
│   │   └── index.ts
│   ├── hooks/
│   │   └── useTodos.ts
│   ├── utils/
│   │   └── localStorage.ts
│   ├── App.tsx
│   └── main.tsx
├── tailwind.config.js
├── tsconfig.json
└── package.json
```

## 3. データモデル

### 3.1 基本データ型

**Todo型**
- id: 一意のID (string)
- text: タスクの内容 (string)
- completed: 完了状態 (boolean)
- createdAt: 作成日時 (Date)

## 4. コンポーネント設計

### 4.1 コンポーネント構成図

```
App
├── Header
├── TodoForm
├── TodoList
│   └── TodoItem (複数)
└── Footer
```

### 4.2 コンポーネント詳細

#### App
- **責務**: アプリケーション全体のレイアウトと状態管理
- **状態**:
  - todos: Todo[] - タスクのリスト
- **機能**:
  - ローカルストレージからのデータ読み込み/保存
  - 子コンポーネントへの状態・関数の受け渡し

#### Header
- **責務**: アプリケーションのタイトル表示
- **状態**: なし
- **props**: なし

#### TodoForm
- **責務**: 新しいタスクの追加フォーム
- **状態**: 
  - text: string - 入力中のテキスト
- **props**: 
  - addTodo: (text: string) => void - タスク追加関数
- **機能**:
  - テキスト入力の管理
  - フォーム送信時のタスク追加処理

#### TodoList
- **責務**: タスクリストの表示
- **状態**: なし
- **props**: 
  - todos: Todo[] - 表示するタスクリスト
  - toggleTodo: (id: string) => void - タスク完了状態切り替え関数
  - deleteTodo: (id: string) => void - タスク削除関数
- **機能**:
  - タスクリストのレンダリング
  - 各TodoItemへのprops受け渡し

#### TodoItem
- **責務**: 個別タスクの表示と操作
- **状態**: なし
- **props**: 
  - todo: Todo - タスク情報
  - toggleTodo: (id: string) => void - 完了状態切り替え関数
  - deleteTodo: (id: string) => void - 削除関数
- **機能**:
  - タスクの表示
  - 完了状態の切り替え
  - タスクの削除

#### Footer
- **責務**: タスク数の表示
- **状態**: なし
- **props**: 
  - activeCount: number - 未完了タスク数
  - totalCount: number - 全タスク数
- **機能**:
  - タスク数の表示

## 5. カスタムフック

### useTodos
- **目的**: Todoリストの状態管理と操作をカプセル化
- **提供する機能**:
  - todos: Todo[] - 現在のタスクリスト
  - addTodo: (text: string) => void - タスク追加
  - toggleTodo: (id: string) => void - 完了状態切り替え
  - deleteTodo: (id: string) => void - タスク削除
  - activeCount: number - 未完了タスク数

## 6. ユーティリティ関数

### localStorage.ts
- **saveTodos**: タスクリストをローカルストレージに保存
- **loadTodos**: ローカルストレージからタスクリストを読み込み

## 7. スタイリング方針

- Tailwind CSSを使用し、モバイルファーストの設計
- 基本カラースキーム:
  - プライマリカラー: 青系 (blue-500)
  - 背景色: 薄いグレー (gray-100)
  - コンテンツ背景: 白 (white)
- レスポンシブ設計:
  - モバイル: 標準表示
  - タブレット/デスクトップ: 最大幅を制限し中央配置

## 8. 実装上の注意点

- コンポーネントの責任を明確に分離する
- Props、状態、型定義を明確にする
- ローカルストレージとの同期を効率的に行う
- パフォーマンスを考慮した実装（不必要な再レンダリングを防ぐ）
