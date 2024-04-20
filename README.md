# kotlin
JetBrainsというチェコの会社が開発したプログラミング言語
- JVMで動作する

## 開発環境

### 環境構築
VSCodeを使って開発環境を作成。  
[参考にした記事](https://zenn.dev/110416/articles/0945183fe53740)

- sdkmanagerをインストール  
  scoopから`android-clt`をインストールし[sdkmanager](https://developer.android.com/tools/sdkmanager?hl=ja)を利用可能とする。

- sdkmanagerを経由してモジュールをインストール
  ```
  sdkmanager --install platform-tools
  sdkmanager --install emulator
  ```

- エミュレーターの作成  
  エミュレーターを作成させるにはシステムイメージが必要なので、検索する。  
  `sdkmanager --list`でシステムを検索。
  
  現状は以下のシステムイメージを取得  
  `sdkmanager --install "system-images;android-34;google_apis_playstore;x86_64"`

  エミュレーターの作成  
  `avdmanager create avd --name android34 --device "pixel"  --package "system-images;android-34;google_apis_playstore;x86_64"`


### ビルドコマンド
- apkファイルのビルド  
  `gradlew :app:assembleDebug`

- エミュレーターの起動  
  `%ANDROID_HOME%\emulator\emulator -avd android34`

- apkファイルのインストール  
  `adb install .\app\build\outputs\apk\debug\app-debug.apk`

- emulator上でのapkファイルの取得
  `adb shell pm list packages -f | findstr com.example.myapplication`

- apkファイルのアンインストール  
  `adb uninstall com.example.myapplication`
