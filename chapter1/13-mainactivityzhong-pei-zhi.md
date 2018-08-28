# MainActivity中配置

#### 1.注册广播接收器

`@Override`

`protected void onCreate(Bundle savedInstanceState) {`

`super.onCreate(savedInstanceState);`

`getWindow().requestFeature(Window.FEATURE_NO_TITLE);`

`getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);`

`/*`

`* 如果不想使用更新流程，可以屏蔽checkApkUpdate函数，一定要把这个游戏自动升级的注释掉`

`*/`

`//checkApkUpdate(this);`

`IntentFilter intentFilter = new IntentFilter(FROM_GAME_ACTION);`

`registerReceiver(mReceiver,intentFilter);`

`  
`

`//initEngine();`

`}`

`/**`

`* 自定义广播接受器,用来处理游戏发过来的消息`

`*/`

`private class GameMessageBroadcastReceiver extends BroadcastReceiver {`

`  
`

`@Override`

`public void onReceive(Context context, Intent intent) {`

`//游戏发送过来的消息`

`if(intent.getAction().equals(FROM_GAME_ACTION)){`

`finish();`

`}`

`  
`

`}`

`}`

#### 2.初始化laya引擎的时候，和游戏交互，传递给游戏数据

`public void initEngine()`

`{`

`mProxy = new RuntimeProxy(this,getIntent().getStringExtra("type"));`

`mPlugin = new GameEngine(this);`

`mPlugin.game_plugin_set_runtime_proxy(mProxy);`

`mPlugin.game_plugin_set_option("localize","true");`

`mPlugin.game_plugin_set_option("gameUrl", "http://stand.alone.version/index.html");`

`mPlugin.game_plugin_init(3);`

`View gameView = mPlugin.game_plugin_get_view();`

`this.setContentView(gameView);`

`new Handler().postDelayed(new Runnable(){`

`public void run() {`

`String isOn=getIntent().getStringExtra("isOn");`

`JSONObject object=new JSONObject();`

`try {`

`object.put\("isOn",isOn\);      
//此为传递数据json字段\`\*\*

`ConchJNI.RunJS("onRecvMessage("+object.toString()+")");`

`} catch (JSONException e) {`

`e.printStackTrace();`

`}`

`  
`

`}`

`},6000);`

`isLoad=true;`

`}`

![](/assets/TIM截图20180828175707.png)

