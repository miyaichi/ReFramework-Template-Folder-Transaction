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

  | TransactionID | TransactionField1 | TransactionField2 |
  | ------------- | ----------------- | ----------------- |
  | ID-1          | File-1            | Ext-1             |


  5. トランザクションテストデータを準備します。

    Test_Framework\_TransactionTest.xsmlにテストデータを準備します。形式は、以下の通り。
    TransactionID, TransactionField1, TransactionField2は、トランザクションデータと同様。Exceptionは、期待する実行結果で以下の3つから選択します。

    * Success: 正常終了
    * BRE: Business Rule Exception
    * AppEx: System Exception

  | TransactionID | TransactionField1 | TransactionField2 | Exception   |
  | ------------- | ----------------- | ----------------- | ----------- |
  | ID-1          | FilePath-1        | Ext-1             | Exception-1 |


  6. トランザクションテストを実施します。

    _TransactionTest.xamlを実行することにより_TransactionTest.xsmlの各行のデータでProcess.xamlをテストします。テスト結果は、Test_Framework\_TransactionTest.xsmlのResultタブと、Test_Framework\TransactionTestLog.txtに出力されます。
