---
title: Xamarinアプリの開始手順 (Getting started with Xamarin apps)
redirect_from: []
date: 2019-03-19 10:35:17 +0000
published: false

---
{% include not_translated_yet.html %}

[Xamarin](/tutorials/xamarin/index/) provides a developer with tools that can help them building cross-platform mobile applications. Bitrise supports Xamarin apps, of course: this guide aims to walk you through the procedure of:

Xamarinはモバイルアプリにおけるクロスプラットフォームのビルド作業のツールを提供しています。もちろんBitriseはXamarinにも対応しています：ここのガイドは以下の手順を説明します：

* adding a Xamarin app to Bitrise
* testing the app
* deploying the app
* BitriseへXamarinアプリの追加
* アプリのテスト
* アプリのデプロイ

You can do the entire procedure in one single workflow but we recommend using at least two: one to test your app and one to deploy it. There is no need to have separate workflows for the different project types, though: you can build both an iOS and an Android version of a Xamarin app within a single workflow.

全ての手順は一つのワークフローで完了できますが、２つ以上のワークフローを使用することをおすすめします：１つ目をアプリのテスト用、２つ目をアプリのデプロイ用としてワークフローを使用してください。異なるプロジェクトであっても、別々のワークフローを用意する必要はありません。iOSとAndroidアプリの両方とも、一つのワークフローでビルドができます。

* [Before you start](/getting-started/getting-started-with-xamarin-apps/#before-you-start)
* [Adding a Xamarin app](/getting-started/getting-started-with-xamarin-apps/#adding-a-xamarin-app)
* [Installing dependencies](/getting-started/getting-started-with-xamarin-apps/#installing-dependencies)
* [Testing Xamarin apps](/getting-started/getting-started-with-xamarin-apps/#testing-xamarin-apps)
* [Deploying Xamarin apps](/getting-started/getting-started-with-xamarin-apps/#deploying-xamarin-apps)
* 始める前に
* Xamarinアプリの追加
* Dependenciesのインストール
* Xamarinアプリのテスト
* Xamarinアプリのデプロイ

## Before you start　始める前に

Before adding a Xamarin app on Bitrise, you need to prepare your Xamarin solution file. Bitrise detects the solution file and all the available [solution configurations](https://docs.microsoft.com/en-us/visualstudio/ide/understanding-build-configurations?view=vs-2017) present in it.

A Xamarin solution file can contain multiple projects. Your solution configuration determines which projects (_solution items_) should be built and what project configuration type (for example, _debug_ or _release_) the build should use.

BitriseへXamarinアプリを追加する前に、Xamarin solution fileを用意する必要があります。Bitriseがそのsolution fileを検知し、全ての利用可能な solution configurationsが表示されます。

Xamarin solution fileは複数のプロジェクトを含めることができます。あなたのsolution configurationがどのプロジェクト（solution items）がビルドされるのか測定し、ビルドする際に使用するproject configuration type（例：_debug_ または _release_）も測定します。

[Set up your solution configurations in Visual Studio](https://docs.microsoft.com/en-us/appcenter/build/xamarin/ios/solution-configuration-mappings). The solution file will have to contain all the solution configurations that you want to build on Bitrise. Also, make sure that a solution configuration you wish to build on a given solution platform is compatible with that platform.

[Visual Studioにてsolution configurationsのセットアップを行ってください](https://docs.microsoft.com/en-us/appcenter/build/xamarin/ios/solution-configuration-mappings)。Solution file上にはBitriseでビルドを行う全てのsolution configurationsが含まれていなければなりません。また、一定のsolution platformでビルドを行う場合、そのプラットフォームに互換性があることを確認してください。

{% include message_box.html type="example" title="Solution configuration" content="For example, if your solution file contains an Android and an iOS project but you want Bitrise to build only the Android project, set up a solution configuration in Visual Studio that only builds the Android project and use that configuration on Bitrise. Use the appropriate solution platform for that configuration: for example, if you only want to build an Android project, do not set iPhone as your solution platform."%}

## Adding a Xamarin app　Xamarinアプリの追加

{% include message_box.html type="note" title="Do you have a Bitrise account?" content=" Make sure you have signed up to [bitrise.io](https://www.bitrise.io) and can access your Bitrise account. Here are [4 ways](/getting-started/index#signing-up-to-bitrise) on how to connect your Bitrise account to your account found on a Git service provider. "%}

 1. Click the `+` sign on the top menu bar and select `Add app`.　上段にあるメニューバーより`+`をクリックして`Add app`を選択します。
 2. On the Create new App page, choose the account you wish to add the app to. Create new Appのページにて、アプリを追加したいアカウントを選んでください。
 3. Set the privacy of the app to either Private or [Public](/getting-started/adding-a-new-app/public-apps) and click `Next`.　アプリのプライバシー設定を行ってください；Private または Publicを選んで`Next`をクリックします。
 4. Select the Git hosting service that hosts your repository, then find and select your repository that hosts the project. Read more about [connecting your repository](/getting-started/adding-a-new-app/connecting-your-repository).　あなたのレポジトリをホストするGit hosting serviceを選択してください。その後、プロジェクトをホストするレポジトリを見つけて選択します。詳しい内容は、[レポジトリに接続する](/getting-started/adding-a-new-app/connecting-your-repository)をお読みください。
 5. When prompted to set up repository access, click `No, auto-add SSH key`. Read more about [SSH keys](/getting-started/adding-a-new-app/setting-up-ssh-keys/).　レポジトリのアクセスのセットアップが完了したら、`No, auto-add SSH key` をクリックします。
 6. Type the name of the branch that includes your project's configuration - master, for example - then click `Next`.　あなたのプロジェクトのconfigurationが含まれたBranchの名前を入力します。
 7. Wait while Bitrise is validating your project. We look for your configuration files and set up your app based on them. In the case of a Xamarin app, we're looking for the Xamarin Solution file.　Bitriseがプロジェクトを確認を行うのでしばらくお待ち下さい。ここではBitriseがconfiguration fileを探して、それに基づいてアプリのセットアップを行います。Xamarinアプリの場合は、Xamarin Solution Fileを探します。
 8. Select the Xamarin solution configuration. The available options are based on the solution file. This will be stored as an [Environment Variable](https://devcenter.bitrise.io/builds/env-vars-secret-env-vars/) and it can be changed later.　Xamarin solution configuration を選択します。利用可能なオプションはsolution fileに基づいています。これは[Environment Variable](https://devcenter.bitrise.io/builds/env-vars-secret-env-vars/)として保存され、あとで変更も可能です。

    ![](/img/xamarin-project-build.png)
 9. Select the Xamarin solution platform. This will be stored as an Environment Variable and it can be changed later.　Xamarin solution platformを選択します。これも[Environment Variable](https://devcenter.bitrise.io/builds/env-vars-secret-env-vars/)として保存され、あとで変更も可能です。
10. Confirm your build configuration.　ビルド設定の最終確認を行ってください。
11. Register a webhook when prompted so that Bitrise can start a build automatically when code is pushed to your repository, or a pull request is created. This also kicks off your first build - click the message and it will take you to the build page.　webhookの登録をしてください。登録後、コードがプッシュされたりプルリクエストが作成されるとBitriseが自動的にビルドを開始します。これで最初のビルドが開始されます。messageをクリックすると、自動的にbuildページに遷移されます。

## Installing dependencies　dependencies のインストール

Installing your dependencies with Xamarin apps is taken care of by a dedicated Step: `NuGet restore`. This Step is part of every automatically created [workflow](/getting-started/getting-started-workflows/) for Xamarin apps and it has one required input: the path to the Xamarin solution file which is stored as an Environment Variable when you add the app.

Xamarinアプリのdependenciesのインストールは特定のステップ`NuGet restore`により処理されます。このステップは自動で作成されたXamarinアプリの[ワークフロー](/getting-started/getting-started-workflows/)の一部を担っており、一つ必要なインプットがあります：アプリを追加する際Environment Variableとして保存されるXamarin solution fileへの進路です。

1. Enter the Workflow Editor of your app, and click the `Workflows` tab.　アプリのWorkflow Editorへ入り、`Workflows`タブをクリックします。
2. Make sure you have the `NuGet restore` Step in your workflow.

   The Step's single required input is the path to the Xamarin solution file. By default, the input is an [Environment Variable](/getting-started/getting-started-steps/#environment-variables-as-step-inputs), stored when adding the app to Bitrise. If you want to use a different solution file, click on the `Env Vars` tab in the Workflow Editor to change the value of the Environment Variable.　あなたのワークフロー内に`NuGet restore`があることを確認してください。ここのステップで必要なインプットはXamarin solution fileへの進路となります。デフォルトでは、そのインプットはEnvironment Variableとなっており、Bitriseにアプリを追加するときに保存されます。異なるsolution fileを使う際は、Workflow Editor内にあるタブ`Env Vars`をクリックして環境変数の値を変更してください。

## Testing Xamarin apps　Xamarinアプリのテスト

You can run **unit tests** and **UI tests** on Bitrise, both with Android and iOS projects. It is easy to configure and you can use all the testing frameworks available on the Microsoft App Center.

BitriseではiOS・Androidプロジェクトの両方でユニットテストとUIテストが行えます。簡単に設定できるので、Microsoft App Centerにて入手可能なTesting Frameworkの全てを利用することができます。

### Unit testing　ユニットテスト

Unit tests of Xamarin apps can be run with the `NUnit Runner` Step. The Step runs NUnit 2.x and NUnit 3.0 or higher tests with the NUnit Console Runner (_nunit3-console.exe_).　

Xamarinアプリのユニットテストは、`NUnit Runner` ステップにて走らせることができます。そのステップはNUnit Console Runnerを使用したNUnit 2.x もしくはNUnit 3.0 またはそれより高いテストで走ります（_nunit3-console.exe_）。

1. Enter the Workflow Editor of your app, and click the `Workflows` tab.　アプリのWorkflow Editorに入り、`Workflows`タブをクリックします。
2. Add the `NUnit runner` Step to your workflow.　

   This Step should be after the `NuGet restore` Step: you will want to install all your dependencies before running tests on your app.　ワークフローに`NUnit runner` ステップを追加します。このステップは`NuGet restore` ステップ後に追加してください：アプリのテストを走らせる前に全てのdependenciesをインストールしてください。
3. Fill in the required input variables. By default, all the inputs are [Environment Variables](/getting-started/getting-started-steps/#environment-variables-as-step-inputs). If you want to use a different solution file or solution configuration, click on the `Env Vars` tab in the Workflow Editor to change the value of the Environment Variable.　必要なinput variablesを入力します。デフォルトでは、全てのinputはEnvironment Variablesになっています。異なるsolution fileまたはsolution configuration を使用する場合は、Workflow Editor内のタブ`Env Vars` をクリックし、環境変数の値を変更してください。
   * **Path to Xamarin Solution**: the location of your Xamarin solution file.　あなたのXamarin solution fileの場所を示します。
   * **Xamarin project configuration**: the solution configuration, set up in Visual Studio, that you want to run on Bitrise. Change the appropriate environment variable if you want to run a different configuration; for example, if you only want to build an iOS project, as opposed to both iOS and Android projects. Bitriseであなたが走らせたい、Visual Studioでセットアップされたsolution configurationが表示されます。異なる設定で走らせたい場合は、適切な環境変数に変更してください。
   * **Xamarin platform**: the target platform of your solution configuration.　あなたのsolution configurationのターゲットプラットフォームを示します。

{% include message_box.html type="note" title="Debug inputs" content="In the Debug input group, you can configure the Step further: set the building tool, set additional flags for the NUnit Console Runner, and configure whether you want to build your test projects before running tests."%}

### UI testing　UIテスト

For UI tests, we strongly recommend using our `App Center upload and schedule tests` Step. You need to set up the tests in the Visual Studio App Center - [read more about it in our guide](/testing/run-your-tests-in-the-app-center/). Let's go through the process in brief.　UIテストでは、Bitrise製の`App Center upload and schedule tests` ステップを使用することを強くお勧めします。Visual Studio App Centerにてテストのセットアップが必要です。詳しくはガイドを参照してください。手順を手短に説明します。

1. Add the `App Center upload and schedule tests` Step to your workflow.

   This Step should be after the `NuGet restore` and the `Xamarin Archive` Steps, in order to install all your dependencies and build the app before running tests.

   あなたのワークフローに`App Center upload and schedule tests` ステップを追加します。

   テストを走らせる前に全てのdependenciesをインストールし、アプリをビルドするため、このステップは、`NuGet restore` 、`Xamarin Archive` ステップの後に追加してください。

   ![](/img/ui-testing-xamarin.png)
2. Fill in the required inputs of the Step. You can find all these in the App Center after setting up your test run: check the **Submit** tab.

   Stepの必要事項の入力を行います。テスト走行をセットした後App Centerにて全て確認することができます：**Submit**タブを確認してください。

If you're interested in Calabash UI testing on Bitrise, check out this [discuss guide](https://discuss.bitrise.io/t/how-to-do-calabash-uitesting-on-bitrise/361)!　BitriseのCalabash UIテストに興味がありましたら、[discuss guide](https://discuss.bitrise.io/t/how-to-do-calabash-uitesting-on-bitrise/361)をチェックしてください。

## Deploying Xamarin apps Xamarinアプリのデプロイ

With the help of Bitrise, you can deploy a Xamarin app to:

Bitriseがあれば、Xamarinアプリを以下の場所へとデプロイが可能です：

* Bitrise.io
* the App Store
* Google Play

To deploy your app, you need to build, sign and export the application file.　アプリをデプロイするには、application fileのビルド、署名、エクスポートが必要です。

### Code signing Xamarin apps　Xamarinアプリのコード署名

Code signing requires different approaches for iOS and Android projects. We're presenting a brief overview here of code signing for both platforms. iOSとAndroidによってコード署名の方法は異なります。双方のプラットフォームでのコード署名方法を説明します。

For the purposes of deploying your app, we recommend [creating a new workflow](/getting-started/getting-started-workflows/), based on the automatically created deploy workflow.　アプリのデプロイが目的であれば、自動で作成されたデプロイワークフローに基づいた、新しいワークフローの作成をおすすめします。

#### **Android**

For Android, you need an APK and you need to sign that APK. Bitrise makes that happen with the `Sign APK` Step. The Step requires a keystore file, a keystore password and a keystore alias.

Android では、APKが必要になり、そのAPKへ署名が必要になります。Bitriseでは`Sign APK` ステップで署名が行なえます。このステップではkeystore ファイル、keystore パスワード、keystore エイリアスが必要です。

1. [Create a code signing identity in Visual Studio](https://docs.microsoft.com/en-us/xamarin/android/deploy-test/signing/?tabs=vswin).

   [Visual Studioにてコード署名のアイデンティティを作成](https://docs.microsoft.com/en-us/xamarin/android/deploy-test/signing/?tabs=vswin)します。
2. Upload the keystore file to Bitrise: open the Workflow Editor of your app, go to the `Code Signing` tab and upload the file to the `ANDROID KEYSTORE FILE` section.

   Bitriseへkeystoreファイルのアップロードを行います：アプリのWorkflow Editorを開いて`Code Signing` タブに進み、`ANDROID KEYSTORE FILE` セクションにファイルのアップロードを行います。
3. Set a keystore password, a keystore alias and a private key password.

   Keystoreパスワード・keystore エイリアス・private key パスワードをそれぞれ入力します。
4. On the `Workflows` tab, add the `Sign APK` Step to your workflow, AFTER the `Xamarin Archive` Step.  `Workflows` タブ上にて、`Xamarin Archive` ステップの**後**に`Sign APK` ステップをワークフローに追加してください。

Read more about using the `Sign APK` Step [in our guide](/code-signing/android-code-signing/android-code-signing-using-bitrise-sign-apk-step/)!

`Sign APK` ステップ使用についての詳細は[ガイド](/code-signing/android-code-signing/android-code-signing-using-bitrise-sign-apk-step/)にてご確認ください。

#### **iOS**

1. Set up your code signing identity and provisioning profile [on Visual Studio](https://docs.microsoft.com/en-us/xamarin/ios/deploy-test/provisioning/).　Visual Studioにて、コード署名アイデンティティとprovisioning profileをセットします。
2. In the solution file, find the iOS project you want to build and set up its project options. You need to set:　solution file
   * the signing identity you want to use (for example, Developer)
   * the provisioning profile

   You can also set up custom entitlements in a .plist file.
3. On your own machine, use our [codesigndoc](https://github.com/bitrise-tools/codesigndoc) tool to collect the code signing files of your project.
4. Upload the files - the .p12 certificate and the provisioning profile - to Bitrise: open the Workflow Editor of your app and upload the files on the `Code Signing` tab.
5. Add the `Certificate and profile installer` Step to your workflow.

Read more about iOS code signing [in our guide](/code-signing/ios-code-signing/create-signed-ipa-for-xamarin/)!

### Exporting the app package file

On Bitrise, it does not matter whether you want to export an .ipa file, an .apk file or an .app file: the process is the same for all Xamarin apps. To make sure you build the correct project type, set up your solution configurations in Visual Studio.

For example, if you want to get an .apk file to upload it to Google Play, use a **Release** project configuration for your Android project in your solution configuration.

For your iOS project, set up the correct code signing identity in Visual Studio: for example, if you want to upload your app to the App Store, use a Distribution identity with an App Store type provisioning profile.

1. Enter the Workflow Editor of your app, and click the `Workflows` tab.
2. Make sure you have the `Xamarin Archive` Step in your workflow.

   ![](/img/xamarin-archive.jpg)
3. Make sure the required inputs of the Step have appropriate values. By default, all the inputs are [Environment Variables](/getting-started/getting-started-steps/#environment-variables-as-step-inputs). Click on the `Env Vars` tab in the Workflow Editor to change the value of the Environment Variable.
   * **Path to the Xamarin Solution file**: the location of your Xamarin solution file.
   * **Xamarin project configuration**: the solution configuration, set up in Visual Studio, that you want to run on Bitrise. Change the appropriate environment variable if you want to run a different configuration; for example, if you only want to build an iOS project, as opposed to both iOS and Android projects.
   * **Xamarin solution platform**: the target platform of your solution configuration.

### Deploying to the App Store

{% include message_box.html type="note" title="Before you start" content="Make sure that you have the correct solution configuration in Visual Studio! You need to use a Distribution type code signing identity with an App Store provisioning profile. Also, make sure that the Distribution certificate and the provisioning profile are uploaded to Bitrise!"%}

1. Go to the `Workflows` tab of the Workflow Editor.
2. Select the workflow you created for deploying your app.
3. Check that the code signing Steps and the `Xamarin Archive` Step are included in the workflow.
4. If you want to use a different solution configuration, change the values of the relevant Environment Variables on the the `Env Var` tab. You can check out which Env Vars you need to change in the inputs of the `Xamarin Archive` Step.
5. Add the `Deploy to iTunes Connect - Application Loader` Step to your workflow.

   ![](/img/deploy-itunes-connect.jpg)
6. Click the `Deploy to iTunes Connect - Application Loader`  Step, and enter your Apple ID and password in the relevant input field.
7. Start a build!

### Deploying to Google Play

{% include message_box.html type="note" title="Before you start" content="Make sure that you have the correct solution configuration in Visual Studio! You need a **Release** configuration."%}

1. Go to the `Workflows` tab of the Workflow Editor.
2. Select the workflow you created for deploying your app.
3. Check that the code signing Steps and the `Xamarin Archive` Step are included in the workflow.
4. If you want to use a different solution configuration, change the values of the relevant Environment Variables on the the `Env Var` tab. You can check out which Env Vars you need to change in the inputs of the `Xamarin Archive` Step.
5. Add the `Google Play Deploy` Step to the workflow.

   The Step needs to be after the `Xamarin Archive` Step.
6. Upload the Service Account JSON key file to the **Generic File Storage** on the `Code Signing`tab of the Workflow Editor.

   Learn more about [how to access your JSON key file](/tutorials/deploy/android-deployment/#set-up-google-play-api-access).
7. Create a Secret Environment Variable to reference the Service Account's JSON key file.
8. Click the `Google Play Deploy` Step, and add the Service Account's JSON key file path and the package name in the relevant input field.
9. Start a build!

If the build is successful, congratulations - you've just deployed your Xamarin app!