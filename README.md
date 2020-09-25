# 【iOS10 Objective-C】プッシュ通知を送ろう！
*2017/02/08更新*

![画像1](/readme-img/001.png)

## 概要
* [ニフクラ mobile backend](https://mbaas.nifcloud.com/)の『プッシュ通知』機能を実装したサンプルプロジェクトです
* 簡単な操作ですぐに [ニフクラ mobile backend](https://mbaas.nifcloud.com/)の機能を体験いただけます★☆
* このサンプルはObjective-C(iOS10)に対応しています
 * Objective-C(iOS10未満)のサンプルは[こちら](https://github.com/NIFCLOUD-mbaas/ObjcPushApp)

## ニフクラ mobile backendって何？？
スマートフォンアプリのバックエンド機能（プッシュ通知・データストア・会員管理・ファイルストア・SNS連携・位置情報検索・スクリプト）が**開発不要**、しかも基本**無料**(注1)で使えるクラウドサービス！

注1：詳しくは[こちら](https://mbaas.nifcloud.com/price.htm)をご覧ください

![画像2](/readme-img/002.png)

## 動作環境
* Mac OS Mojave
* Xcode ver. 11.0 
* iPhone6s(iOS 13.1)
 * このサンプルアプリは、実機ビルドが必要です

※上記内容で動作確認をしています

## プッシュ通知の仕組み
* ニフクラ mobile backendのプッシュ通知は、iOSが提供している通知サービスを利用しています
 * iOSの通知サービス　__APNs（Apple Push Notification Service）__

 ![画像1](/readme-img/001.png)

* 上図のように、アプリ（Xcode）・サーバー（ニフクラ mobile backend）・通知サービス（APNs）の間でやり取りを行うため、認証が必要になります
 * 認証に必要な鍵や証明書の作成は作業手順の「0.プッシュ通知機能を使うための準備」で行います

## 作業の手順
### 0.プッシュ通知機能を使うための準備
__[【iOS】プッシュ通知の受信に必要な証明書の作り方(開発用)](https://github.com/NIFCLOUD-mbaas/iOS_Certificate)__
* 上記のドキュメントをご覧の上、必要な証明書類の作成をお願いします
 * 証明書の作成には[Apple Developer Program](https://developer.apple.com/account/)の登録（有料）が必要です

![画像i002](/readme-img/i002.png)

### 1. [ニフクラ mobile backend](https://mbaas.nifcloud.com/)の会員登録とログイン→アプリ作成と設定
* 上記リンクから会員登録（無料）をします。登録ができたらログインをすると下図のように「アプリの新規作成」画面が出るのでアプリを作成します

![画像3](/readme-img/003.png)

* アプリ作成されると下図のような画面になります
* この２種類のAPIキー（アプリケーションキーとクライアントキー）はXcodeで作成するiOSアプリに[ニフクラ mobile backend](https://mbaas.nifcloud.com/)を紐付けるために使用します

![画像4](/readme-img/004.png)

* 続けてプッシュ通知の設定を行います
* ここで⑦APNs用証明書(.p12)の設定も行います

![画像5](/readme-img/005.png)

### 2. [GitHub](https://github.com/NIFCLOUD-mbaas/ObjcPushApp_iOS10.git)からサンプルプロジェクトのダウンロード

* 下記リンクをクリックしてプロジェクトをMacにダウンロードします
  * https://github.com/NIFCLOUD-mbaas/ObjcPushApp_iOS10/archive/master.zip

### 3. Xcodeでアプリを起動

* ダウンロードしたフォルダを開き、「__ObjcPushApp_iOS10.xcworkspace__」をダブルクリックしてXcode開きます(白い方です)

![画像09](/readme-img/009.png)
![画像06](/readme-img/006.png)

* 「ObjcPushApp_iOS10.xcodeproj」（青い方）ではないので注意してください！

![画像08](/readme-img/008.png)

### 4. APIキーの設定

* `AppDelegate.m`を編集します
* 先程[ニフクラ mobile backend](https://mbaas.nifcloud.com/)のダッシュボード上で確認したAPIキーを貼り付けます

![画像07](/readme-img/007.png)

* それぞれ`YOUR_NCMB_APPLICATION_KEY`と`YOUR_NCMB_CLIENT_KEY`の部分を書き換えます
 * このとき、ダブルクォーテーション（`"`）を消さないように注意してください！
* 書き換え終わったら`command + s`キーで保存をします

### 5. 実機ビルド
* 始めて実機ビルドをする場合は、Xcodeにアカウント（AppleID）の登録をします
 * メニューバーの「Xcode」＞「Preferences...」を選択します
 * Accounts画面が開いたら、左下の「＋」をクリックします。
 * Apple IDとPasswordを入力して、「Add」をクリックします

 ![画像i29](/readme-img/i029.png)

 * 追加されると、下図のようになります。追加した情報があっていればOKです
 * 確認できたら閉じます。

 ![画像i30](/readme-img/i030.png)

* 「TARGETS」 ＞「General」を開きます

![画像14](/readme-img/014.png)

* 「Identity」＞「Bundle Identifier」を入力します
 * 「Bundle Identifier」にはAppID作成時に指定した「Bundle ID」を入力してください
* 「Signing(Debug)」＞「Provisioning Profile」を設定します
 * 今回使用するプロビジョニングプロファイルをプルダウンから選択します
 * プロビジョニングプロファイルはダウンロードしたものを一度__ダブルクリック__して認識させておく必要があります（プルダウンに表示されない場合はダブルクリックを実施後設定してください）
 * 選択すると以下のようになります
 ![画像15](/readme-img/015.png)

* 「TARGETS」＞「Capabilities」を開き、「Push Notifications」を__ON__に設定します
 * 設定すると以下のようになります
 ![画像16](/readme-img/016.png)

* 設定は完了です
* lightningケーブルで登録した動作確認用iPhoneをMacにつなぎます
* Xcode画面で左上で、接続したiPhoneを選び、実行ボタン（さんかくの再生マーク）をクリックします

### 6.動作確認
* インストールしたアプリを起動します
 * プッシュ通知の許可を求めるアラートが出たら、必ず許可してください！
* 起動されたらこの時点でデバイストークンが取得されます
* [ニフクラ mobile backend](https://mbaas.nifcloud.com/)のダッシュボードで「データストア」＞「installation」クラスを確認してみましょう！

![画像12](/readme-img/012.png)

* 端末側で起動したアプリは一度閉じておきます

### 7.__プッシュ通知を送りましょう！__
* いよいよです！実際にプッシュ通知を送ってみましょう！
* [ニフクラ mobile backend](https://mbaas.nifcloud.com/)のダッシュボードで「プッシュ通知」＞「＋新しいプッシュ通知」をクリックします
* プッシュ通知のフォームが開かれます
* 必要な項目を入力してプッシュ通知を作成します

![画像13](/readme-img/013.png)

* 端末を確認しましょう！
* 少し待つとプッシュ通知が届きます！！！

![画像17](/readme-img/017.png)

## 解説
サンプルプロジェクトに実装済みの内容のご紹介

#### SDKのインポートと初期設定
* ニフクラ mobile backend の[ドキュメント（クイックスタート）](https://mbaas.nifcloud.com/doc/current/introduction/quickstart_ios.html)をご活用ください

#### ロジック
 * `AppDelegate.m`の`didFinishLaunchingWithOptions`メソッドにAPNsに対してデバイストークンの要求するコードを記述し、デバイストークンが取得された後に呼び出される`didRegisterForRemoteNotificationsWithDeviceToken`メソッドを追記をします
 * デバイストークンの要求はiOSのバージョンによってコードが異なります

```Objective-C
#import "AppDelegate.h"
#import <UserNotifications/UserNotifications.h>
#import <NCMB/NCMB.h>

@interface AppDelegate ()

@end

@implementation AppDelegate


- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // APIキーの設定とSDK初期化
    [NCMB setApplicationKey:@"YOUR_APPLICATION_KEY" clientKey:@"YOUR_CLIENT_KEY"];

    // デバイストークンの要求
    if ([[NSProcessInfo processInfo] isOperatingSystemAtLeastVersion:(NSOperatingSystemVersion){10, 0, 0}]){
        /** iOS10以上 **/
        UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
        [center requestAuthorizationWithOptions:(UNAuthorizationOptionAlert | UNAuthorizationOptionBadge | UNAuthorizationOptionSound) completionHandler:^(BOOL granted, NSError * _Nullable error) {
            if (error) {
                // エラー時の処理

                return;
            }
            if (granted) {
                // デバイストークンの要求
                [[UIApplication sharedApplication] registerForRemoteNotifications];
            }
        }];
    } else {
        /** iOS8以上iOS10未満 **/
        //通知のタイプを設定したsettingを用意
        UIUserNotificationType type = UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound;
        UIUserNotificationSettings *setting = [UIUserNotificationSettings settingsForTypes:type categories:nil];
        //通知のタイプを設定
        [[UIApplication sharedApplication] registerUserNotificationSettings:setting];
        //DeviceTokenを要求
        [[UIApplication sharedApplication] registerForRemoteNotifications];
    }

    return YES;
}

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    //端末情報を扱うNCMBInstallationのインスタンスを作成
    NCMBInstallation *installation = [NCMBInstallation currentInstallation];
    //Device Tokenを設定
    [installation setDeviceTokenFromData:deviceToken];
    //端末情報をデータストアに登録
    [installation saveInBackgroundWithBlock:^(NSError *error) {
        if(!error){
            //端末情報の登録が成功した場合の処理
        } else {
            //端末情報の登録が失敗した場合の処理
        }
    }];
}

@end
```

## 参考
* 同じ内容の【Swift3(iOS10)】版もご用意しています
 * [Swift3PushApp](https://github.com/NIFCLOUD-mbaas/Swift3PushApp)
* ニフクラ mobile backend の[ドキュメント（プッシュ通知）](https://mbaas.nifcloud.com/doc/current/push/basic_usage_ios.html)をSwift版に書き換えたドキュメントをご用意していますので、ご活用ください
 * [Swift2(iOS9,8)] [Swiftでプッシュ通知を送ろう！](http://qiita.com/natsumo/items/8ffafee05cb7eb69d815)
