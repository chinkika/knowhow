
#### UnreachableBrowserExceptionエラー詳細 ####
```
org.openqa.selenium.remote.UnreachableBrowserException: Error communicating with the remote browser. It may have died.
Build info: version: '2.53.0', revision: '35ae25b', time: '2016-03-15 17:00:58'
System info: host: 'NAR-CLP103.local', ip: '192.168.13.120', os.name: 'Mac OS X', os.arch: 'x86_64', os.version: '10.13.6', java.version: '1.8.0_152'
Driver info: driver.version: AndroidDriver
Capabilities [{appPackage=jp.co.sharp.printsystem.networkprint, statBarHeight=72, noReset=true, viewportRect={top=72, left=0, width=1080, height=1776}, deviceName=353479090091108, platform=LINUX, deviceUDID=353479090091108, desired={appPackage=jp.co.sharp.printsystem.networkprint, appActivity=jp.co.sharp.printsystem.networkprint.NetworkPrintActivity, noReset=true, platformVersion=8.0.0, automationName=UiAutomator2, sessionOverride=true, platformName=Android, deviceName=353479090091108}, platformVersion=8.0.0, webStorageEnabled=false, automationName=UiAutomator2, takesScreenshot=true, javascriptEnabled=true, platformName=Android, deviceApiLevel=26, deviceManufacturer=SHARP, deviceScreenSize=1080x1920, networkConnectionEnabled=true, warnings={}, databaseEnabled=false, appActivity=jp.co.sharp.printsystem.networkprint.NetworkPrintActivity, pixelRatio=3, locationContextEnabled=false, deviceScreenDensity=480, deviceModel=SH-M06, sessionOverride=true}]
Session ID: f1a379e0-d10a-4b3b-9fb4-f66705f11591
	at org.openqa.selenium.remote.RemoteWebDriver.execute(RemoteWebDriver.java:665)
	at io.appium.java_client.DefaultGenericMobileDriver.execute(DefaultGenericMobileDriver.java:27)
	at io.appium.java_client.AppiumDriver.execute(AppiumDriver.java:1)
	at io.appium.java_client.android.AndroidDriver.execute(AndroidDriver.java:1)
	at org.openqa.selenium.remote.RemoteWebDriver.findElement(RemoteWebDriver.java:363)
	at org.openqa.selenium.remote.RemoteWebDriver.findElementByXPath(RemoteWebDriver.java:500)
	at io.appium.java_client.DefaultGenericMobileDriver.findElementByXPath(DefaultGenericMobileDriver.java:99)
	at io.appium.java_client.AppiumDriver.findElementByXPath(AppiumDriver.java:1)
	at io.appium.java_client.android.AndroidDriver.findElementByXPath(AndroidDriver.java:1)
	at utils.UIExecutorImpl.getElement(UIExecutorImpl.java:113)
	at utils.UIExecutorImpl$1.apply(UIExecutorImpl.java:35)
	at utils.UIExecutorImpl$1.apply(UIExecutorImpl.java:1)
	at org.openqa.selenium.support.ui.FluentWait.until(FluentWait.java:238)
	at utils.UIExecutorImpl.click(UIExecutorImpl.java:32)
	at object.BasePage.click(BasePage.java:26)
	at testcase.basicTest.fileSelectOneFromTop(basicTest.java:315)
	at testcase.basicTest.fileSelectOne(basicTest.java:243)
	at testcase.basicTest.smoketest(basicTest.java:85)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:50)
	at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
	at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:47)
	at org.junit.internal.runners.statements.InvokeMethod.evaluate(InvokeMethod.java:17)
	at org.junit.internal.runners.statements.RunBefores.evaluate(RunBefores.java:26)
	at org.junit.internal.runners.statements.RunAfters.evaluate(RunAfters.java:27)
	at org.junit.runners.ParentRunner.runLeaf(ParentRunner.java:325)
	at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:78)
	at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:57)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
	at org.eclipse.jdt.internal.junit4.runner.JUnit4TestReference.run(JUnit4TestReference.java:86)
	at org.eclipse.jdt.internal.junit.runner.TestExecution.run(TestExecution.java:38)
	at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.runTests(RemoteTestRunner.java:538)
	at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.runTests(RemoteTestRunner.java:760)
	at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.run(RemoteTestRunner.java:460)
	at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.main(RemoteTestRunner.java:206)
Caused by: java.net.SocketException: Connection reset
	at java.net.SocketInputStream.read(SocketInputStream.java:210)
	at java.net.SocketInputStream.read(SocketInputStream.java:141)
	at org.apache.http.impl.io.SessionInputBufferImpl.streamRead(SessionInputBufferImpl.java:139)
	at org.apache.http.impl.io.SessionInputBufferImpl.fillBuffer(SessionInputBufferImpl.java:155)
	at org.apache.http.impl.io.SessionInputBufferImpl.readLine(SessionInputBufferImpl.java:284)
	at org.apache.http.impl.conn.DefaultHttpResponseParser.parseHead(DefaultHttpResponseParser.java:140)
	at org.apache.http.impl.conn.DefaultHttpResponseParser.parseHead(DefaultHttpResponseParser.java:57)
	at org.apache.http.impl.io.AbstractMessageParser.parse(AbstractMessageParser.java:261)
	at org.apache.http.impl.DefaultBHttpClientConnection.receiveResponseHeader(DefaultBHttpClientConnection.java:165)
	at org.apache.http.impl.conn.CPoolProxy.receiveResponseHeader(CPoolProxy.java:167)
	at org.apache.http.protocol.HttpRequestExecutor.doReceiveResponse(HttpRequestExecutor.java:272)
	at org.apache.http.protocol.HttpRequestExecutor.execute(HttpRequestExecutor.java:124)
	at org.apache.http.impl.execchain.MainClientExec.execute(MainClientExec.java:271)
	at org.apache.http.impl.execchain.ProtocolExec.execute(ProtocolExec.java:184)
	at org.apache.http.impl.execchain.RetryExec.execute(RetryExec.java:88)
	at org.apache.http.impl.execchain.RedirectExec.execute(RedirectExec.java:110)
	at org.apache.http.impl.client.InternalHttpClient.doExecute(InternalHttpClient.java:184)
	at org.apache.http.impl.client.CloseableHttpClient.execute(CloseableHttpClient.java:71)
	at org.apache.http.impl.client.CloseableHttpClient.execute(CloseableHttpClient.java:55)
	at org.openqa.selenium.remote.internal.ApacheHttpClient.fallBackExecute(ApacheHttpClient.java:144)
	at org.openqa.selenium.remote.internal.ApacheHttpClient.execute(ApacheHttpClient.java:90)
	at org.openqa.selenium.remote.HttpCommandExecutor.execute(HttpCommandExecutor.java:142)
	at org.openqa.selenium.remote.RemoteWebDriver.execute(RemoteWebDriver.java:644)
	... 42 more

```


#### 試した対応 ####
- １、selenium接続タイムアウト、タイムアウト時間を延ばしてみる
```
System.setProperty("sun.net.client.defaultConnectTimeout", "95000");
System.setProperty("sun.net.client.defaultReadTimeout", "95000");
```
  - https://blog.csdn.net/xiaomin1991222/article/details/50979963
  - 結果：効果なし


- ２、TCP接続数オーバー、TCP接続可能数を増やしてみる(128→2048→4096)
```
$ sysctl -a | grep somax
kern.ipc.somaxconn: 128
$ sudo sysctl -w kern.ipc.somaxconn=2048
```
  - https://blog.csdn.net/pehaps/article/details/8818890
  - http://www.cnblogs.com/olartan/p/4268269.html
  - 結果：効果なし


- ３、ライブラリ古い、更新してみる
  - selenium-java-3.11.0.jar　→　selenium-java-3.12.0.jar
  - Appium/appiumDesk1.9.0　→　最新1.10.0
  - 結果：効果なし


- ４、Appium出力ログが多すぎで、メモリ圧迫、ログを吐かないようにしてみる
```
/Applications/Appium.app/Contents/Resources/app/node_modules/appium-adb/build/lib/logcat.js
/Applications/Appium.app/Contents/Resources/app/node_modules/appium-adb/lib/logcat.js
```
  - 上記二ファイルにpush logのところ注釈
  - https://blog.csdn.net/qq_15283475/article/details/80404063
  - 結果：効果ある？(出る回数が減っている？)


- ５、関係そうな要素取得する方法を変更
  - id/xpath
  - xpathの場合、画面変わったら同じ要素のxpath変わるかもしれない為、要確認
