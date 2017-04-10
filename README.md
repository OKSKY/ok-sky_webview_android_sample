== README 

AndroidでOK SKYを使用するためのサンプルコードです。  
サンプルコードの処理を追加することで、以下のことが可能になります。  
・ファイルアップロード  
・リンクを含むメッセージでのHTTPコンテンツの表示  

**サンプルコードで対象としているAndroidのバージョン**  
Android 4.4 (KitKat) 以上

**サンプルコードで必要なJDK**  
JDK 1.6以上

**サンプルコードで必要なjarファイル**  
commons-io-2.5.jar

**サンプルコード追加手順**  
MainActivity.java  
(<https://github.com/OKSKY/ok-sky_webview_android_sample/blob/master/app/src/main/java/solairo/oksky/MainActivity.java>)  
を参考にして、  
以下の内容を追加してください。

1. WebViewのインスタンスに、setWebChromeClientで、WebChromeClientのインスタンスをセットする。  
(onShowFileChooserなどの、サンプルコードに記載したメソッドをOverrideする。)
2. onActivityResultに、ダイアログでファイルが選択された場合の処理を追加する。  
(onActivityResultがない場合は、新しく作成する。)
3. 1、2の手順で追加した処理で使用されているフィールドを追加する。
4. webViewのインスタンスから、getSettingsでWebSettingsのインスタンスを取得し、  
WebSettingsのインスタンスにsetMixedContentModeで、WebSettings.MIXED_CONTENT_COMPATIBILITY_MODEをセットする。

**処理についての説明**  
`openFileChooser(ValueCallback<Uri> uploadMsg)`  
Android 2.2 から Android 2.3 で、  
input type="file"の選択ボタンが押された場合に呼び出される処理です。  
サンプルコードでは、対象のOSのバージョンをサポートしていない旨のポップアップを表示させています。

`openFileChooser(ValueCallback uploadMsg, String acceptType)`  
Android 3.0 から Android 4.0 で、  
input type="file"の選択ボタンが押された場合に呼び出される処理です。  
サンプルコードでは、対象のOSのバージョンをサポートしていない旨のポップアップを表示させています。

`openFileChooser(ValueCallback<Uri> uploadMsg, String acceptType, String capture)`  
Android 4.1 から Android 4.4 で、  
input type="file"の選択ボタンが押された場合に呼び出される処理です。  
サンプルコードでは、Android 4.4 以外の場合に、対象のOSのバージョンをサポートしていない旨のポップアップを表示させています。

`onShowFileChooser(WebView webView, ValueCallback<Uri[]> filePathCallback, WebChromeClient.FileChooserParams fileChooserParams)`  
Android 5.0以上で、input type="file"の選択ボタンが押された場合に呼び出される処理です。

`onActivityResult(int requestCode, int resultCode, Intent intent)`  
ファイル選択ダイアログでファイルが選択された場合に呼び出される処理です。  
2つ目の引数のresultCodeに、startActivityForResultで指定したcodeが渡されます。  
その値を使用して、実行された処理がファイルアップロードであることを判別します。

`setMixedContentMode(int mode)`  
安全でないオリジンからのコンテンツの読み込みを許可するかを指定します。  
Android 5.0以上では、デフォルトでMIXED_CONTENT_NEVER_ALLOWが設定されているので、  
MIXED_CONTENT_COMPATIBILITY_MODEをセットすることで、  
HTTPコンテンツの読み込みを可能にします。

**フィールドについての説明**  
`ValueCallback<Uri> mUploadMessage`  
Android 4.4 でファイルアップロードが行われた場合に、  
ファイルに関連するデータを保持するためのフィールドです。

`ValueCallback<Uri[]> mFilePathCallback`  
Android 5.0 以上でファイルアップロードが行われた場合に、  
ファイルに関連するデータを保持するためのフィールドです。

`Map<String, String> extensionMap`  
OK SKYでサポートしているContent-Type、拡張子のMapです。  
サンプルコードでは、ファイル名に拡張子がついているファイルのみを、  
アップロードの対象としています。


## Google Cloud Messaging

<span