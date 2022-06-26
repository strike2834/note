# [良いコードとは何か](https://speakerdeck.com/moriatsushi/liang-ikodotohahe-ka-enziniaxin-zu-yan-xiu-suraidogong-kai)

- [質とスピード（2022春版、質疑応答用資料付き） / Quality and Speed 2022 Spring Edition - Speaker Deck](https://speakerdeck.com/twada/quality-and-speed-2022-spring-edition)
- 品質和時間之間的關係並不對等
- 提高品質需要的是知識／經驗
- 可透過內聚性與耦合性等指標，評價模組的品質
- 分離關注點，控制正確依賴方向，實現乾淨架構
- 命名、註解、Code Review...etc. 提昇品質需要龐大的知識

## 內聚性

- 分析模組內（單一模組）的協調性
- 內聚性高的模組通常會有強健性、可靠性、可複用性、易懂性等特點
- 單一功能原則（SOLID）
- 偶然內聚性
  - 模組中的功能只是剛好放在一起。
  - 模組內的各部份沒有關聯性。
  - 「總之可以用」
  ```
    fun main() {
      val data = getData()   // 取得資料
      println("Hello World") // 輸出
      calcPrimeNumber(10)    // 計算質數
  }
  ```
- 邏輯內聚性
  - 模組內的功能在邏輯上類似。
  - 例如判斷 flag 執行不同的動作
  ```
    fun sample(isA: Boolean) {
      if (isA) {
        sampleA()
      } else {
        sampleB()
      }
    }
  ```
- 時間內聚性
  - 模組內的功能在執行時間點上類似。
  - 即使替換執行順序也能正常運作。
  - 例如初始化處理、UI 要前景化時的處理等等
  ```
    fun initApp(isA: Boolean) {
      initConfig()
      initLogger()
      initDB()
    }
  ```
- 程式內聚性
  - 模組內的功能必須依照固定順序執行
  - 例如確認存取權限後修改檔案
  ```
    fun outputFile(file: File) {
      checkPermission()
      writeFile(file)
    }
  ```
- 聯絡內聚性
  - 模組內的功能處理相同的資料
  ```
    fun changeAll(data: Data) {
      changeA(data)
      changeB(data)
      changeC(data)
    }
  ```
- 依序內聚性
  - 模組內的功能整合了一部分的輸入與一部分的輸出
  - 例如取得檔案後做轉換並儲存
  ```
    fun sample() {
      val file = getFile()
      val transformed = transform(file)
      saveFile(transformed)
    }
  ```
- 功能內聚性
  - 模組內的功能處理了單一有明確定義的任務
  - 例如計算兩點之間的距離
  ```
    fun calcLength(a: Point, b: Point): Int {
      val dx = a.x - b.x
      val dy = a.y - b.y
      val length = sqrt(dx * dx + dy * dy)
      return length.toInt()
    }
  ```

## 耦合性

- 分析模組間（多個模組）的依賴性
- 耦合性越低則通常可讀性及可維護性會越高
- 與內聚性有高關聯性，通常內聚性越高則耦合性也會越低
- 內容耦合
  - 模組須依賴於其他模組，或因為其他模組內部執行而有不同變化
  - 例如反射式編程，直接參照其他模組的內部資料
  ```
    fun updatePrivateVariable() {
      val data = Data()
      val property = data::class.memberProperties
          .first { it.name == "value" } as KMutableProperty<*>
      property.isAccessible = true
      val updated = Value()
      property.setter.call(data, updated)
    }
  ```
- 共享耦合
  - 多個模組會一同存取同個全域資料的狀態
  - 當加上變更時，可能會導致無法預期的副作用
  ```
    val data: Data = Data()
    fun updateA() {
      data.value = "a"
    }
    fun updateB() {
      data.value = "b"
    }
  ```
- 外部耦合
  - 模組共享全域狀態的標準化界面
  - 可能會導致發生與外部工具或外部裝置的連線
  ```
    fun function1() {
      Api.getData()
    }
    fun function2() {
      Api.update(Data())
    }
  ```
- 控制耦合

  - 模組傳遞控制關聯的資訊給另一個模組，藉此控制該模組的處理流程
  - 會造成邏輯內聚性

  ```
    fun function1() {
      function2(true)
    }

    fun function2(flag: Boolean) {
      if (flag) {
        println("A")
      } else {
        println("B")
      }
    }
  ```

- 特徵耦合
  - 模組以 class 等資料結構傳遞資料
  - 可能因此傳出不必要的資料
  ```
    fun function1() {
      function2(User(name = "Mori Atsushi"))
    }
  ```
- 資料耦合
  - 模組僅傳入基本參數
  - 只傳遞最低限度需要的資料
  ```
    fun function1() {
      function2(123, "abc")
    }
  ```
- 訊息耦合
  - 模組不傳入參數
  - 不存在資料的傳遞行為
  ```
    fun function1() {
      function2()
    }
  ```
