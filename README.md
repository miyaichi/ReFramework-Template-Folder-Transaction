# ReFramework Template Folder Transaction

フォルダーのファイルをトランザクションとして処理するワークフローテンプレート

指定したフォルダーに格納されたファイルを順に処理するような場合に利用します。

## 設定

Data¥Condig.xlsxで以下の設定ができます。

Settingタブ

| Name                     | Default                   | Description                                 |
|:-------------------------|:--------------------------|:--------------------------------------------|
| logF_BusinessProcessName | Framework Folder Template | ワークフローの名称（ログに出力されます）    |
| FolderPath               | Data\Input                | フォルダのパス                              |
| FilePatternList          | *.*                       | ファイルパターン（複数の場合は「,」区切り） |
| ArchivePath              | Data\Archive              | 処理済みファイルの移動先                    |

Constantsタブ

| Name           | Default | Description  |
|:---------------|:--------|:-------------|
| MaxRetryNumber | 3       | リトライ回数 |

## 利用方法

1. テンプレート一式をダウンロードします。

2. project.jsonの"name","description"を修正します。

3. Data¥Config.xslxに対象とするフォルダ名、ファイルパターン（複数の場合は、*.csv,*.tsvのようにカンマで区切ります）

4. Process.xamlを実装します。

  in_TransactionItem（DataRow型）にトランザクションデータ（ファイル名と拡張子）が渡されます。データの不備等で処理を再実行できない場合は、BRE(Business Rule Exception)をThrowするように実装してください。

| TransactionID | Path   | Extension |
|:--------------|:-------|:----------|
| ID-1          | File-1 | Ext-1     |
