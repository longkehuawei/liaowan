# RuntimeProxy 配置

#### 1.构造方法加入WeakReference ，能够释放Activity,防止内存泄漏

`private static WeakReference<Activity> mActivity = null;`

`private static String type;//游戏类型 单机还是pK`

`public RuntimeProxy(Activity mainActivity,String type) {`

`this.mActivity = new WeakReference<>( mainActivity);`

`this.type=type;`

`}`

#### 2.laya调用java静态方法

`public static void SendMessageToPlatform(JSONObject jsonObj) {`

`/* {"game_type":'laya',"age":20,"id":1001}*/`

`if (mActivity!=null&&mActivity.get() != null){`

`LocalBroadcastManager.getInstance(mActivity.get()).sendBroadcast(`

`new Intent(FROM_GAME_ACTION).putExtra("data",jsonObj.toString()).putExtra("type",type)`

`);`

` `

`}`

`  
`

`}`

