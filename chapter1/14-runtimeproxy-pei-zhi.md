# RuntimeProxy 配置

#### 1.构造方法加入WeakReference ，能够释放Activity,防止内存泄漏

`private static WeakReference<Activity> mActivity = null;`

`private static String type;//游戏类型 单机还是pK`

`public RuntimeProxy(Activity mainActivity,String type) {`

`this.mActivity = new WeakReference<>( mainActivity);`

`this.type=type;`

`}`

#### 2.laya调用对象方法获取平台信息

---

* ##### **进入游戏，游戏主动拉取平台数据**

* ##### 数据格式如下:

         **{"voice":"0","time":"40","model":"PK","pkId":"519092747169701888"}**

         **voice:0表示音乐关，1表示音乐开启**

         **time：时间单位为S**

         **modle:PK表示游戏当前为PK模式，SINGLE为单机模式**

public  String GetPlatformInfo\(\) {

```
    ExportJavaFunction.CallBackToJS \(this, "GetPlatformInfo", data\);

    try {

        JSONObject object=new JSONObject\(data\);

        if\(object.has\("model"\)\){

            String model =object.getString\("model"\);

            if\(model.equals\("PK"\)\){

                EventBus.getDefault\(\).post\(new MessageEvent\(""\)\);

            }

        }



    } catch \(JSONException e\) {

        e.printStackTrace\(\);

    }



    return data;

}
```



