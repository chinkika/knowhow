

#### 作業時のメモ_python_selenium ####


##### 1.環境構築
- centos7で試してみた
```
Python: 2.7.5
selenium: 3.141.0
ChromeDriver: 79.0.3945.36
Chrome: 79.0.3945.88
```
- https://qiita.com/mindwood/items/245adeb6da18999bbfc4
- https://www.htmlhifive.com/conts/web/view/library/webdriver-howtouse


##### 2.python
- 初期設定
```
# coding: utf-8
↑一番最初にコードを指定しないといけない
#====================
options = webdriver.ChromeOptions()
#options.add_argument('--headless')
options.add_argument('--no-sandbox')
driver = webdriver.Chrome(executable_path='/usr/lib/python2.7/site-packages/chromedriver_binary/chromedriver', options=options)
```
  - #はコメントで、headlessコメントアウトした場合UI画面が出る、なければ画面無裏で処理されている
  - chromedriverパスは自分の環境に合わせて修正


- 基本構成
  - 開始と終了
  ```
  driver.get(url)
  ：
  driver.close()
  ```
  - tryとexception
  ```
  try:
    WebDriverWait(driver, time_to_wait).until(EC.presence_of_all_elements_located)
    driver.find_element_by_link_text('logout').click()
  except:
    if result == 0:
        result = 1
    print('logout fail!')
  sys.exit(result)←結果をシステムパラメータに保存、$?で取得できる
  ```


- 実行方法
```
python sample.py
```


##### 3.selenium
- 要素取得
```
タグで指定する場合
driver.find_elements_by_tag_name("h2")
クラスの指定
driver.find_elements_by_class_name("panel-title")
CSSセレクタ
driver.find_elements_by_css_selector("h2.panel-title")
xpath
driver.find_elements_by_xpath("//h2[@class='panel-title']")
====================
find_element_by_id
find_element_by_name
find_element_by_xpath
find_element_by_link_text
find_element_by_partial_link_text
find_element_by_tag_name
find_element_by_class_name
find_element_by_css_selector
====================
elements 複数、「リスト」が返る
find_elements_by_name
find_elements_by_xpath
find_elements_by_link_text
find_elements_by_partial_link_text
find_elements_by_tag_name
find_elements_by_class_name
find_elements_by_css_selector
```


- 入力やクリック処理
```
driver.find_element_by_name('password').clear()
driver.find_element_by_name('password').send_keys('abc')
driver.find_element_by_name('login').click()
↑シングル・ダブルクォーテーション両方使える
```


- selectボックス値設定処理
```
from selenium.webdriver.support.select import Select
lang = Select(driver.find_element_by_id('lang'))
lang.select_by_value('us')
```


- リンク付きのタブをクリック
```
driver.find_element_by_link_text('Product Key').click()
```


- テーブルのtr/tdを探す処理
```
table = driver.find_element_by_class_name('list')
trs = table.find_element_by_tag_name('tbody').find_elements_by_tag_name('tr')
checkCount = 0
for tr in trs:
	td = tr.find_element_by_tag_name('td')
	if td.text == 'id':
		checkCount += 1
	elif td.text == 'serial':
		checkCount += 1
if checkCount != 2:
	raise ValueError('value error')
```
  - 英語の比較は==/!=で問題ないが、日本語の場合UnicodeDecodeErrorが出る。
  - ↑解決方法：encodeを追加
  ```
  if ele.get_attribute('value').encode('utf_8') == '日本語':
    element = ele
    break
  if element is None:
    raise ValueError('Yes button none!')
  ```
  - https://cocodrips.hateblo.jp/entry/2014/03/20/193240
  - raise ValueErrorは手動でexceptionを出す


- 遅延処理
  - Pythonでsleepを使う書き方
  ```
  import time
  time.sleep(秒数)
  ```
  - 画面が全部表示されるまでのwait処理
  ```
  from selenium.webdriver.support.ui import WebDriverWait
  from selenium.webdriver.support import expected_conditions as EC
  from selenium.common.exceptions import TimeoutException
  time_to_wait = 20
  driver.set_page_load_timeout(time_to_wait)
  driver.implicitly_wait(time_to_wait)
  WebDriverWait(driver, time_to_wait).until(EC.presence_of_all_elements_located)
  ```


##### 4.参考になるリンク
- seleniumクイックレファレンス
https://www.seleniumqref.com/api/python/window_set/Python_close.html
- 要素取得方法等の基本
https://narito.ninja/blog/detail/69/
