# MainActivity中配置

#### 1.处理平台消息

/\*\*

```
 \* 处理平台消息

 \*/
```

`private class GameMessageBroadcastReceiver extends BroadcastReceiver {`

`@Override`

`public void onReceive(Context context, Intent intent) {`

`//游戏发送过来的消息`

`if(intent.getAction().equals(FROM_GAME_ACTION)){`

`if(intent.getStringExtra("type").equals("finish")){`

`finish();`

`new Handler().postDelayed(new Runnable() {`

`@Override`

`public void run() {`

`int pid = android.os.Process.myPid();`

`Log.e("message", "Logout SendMessageToPlatform = "+pid);`

`android.os.Process.killProcess(pid);`

`}`

`}, 100);`

`}else{`

`String score= intent.getStringExtra("score");`

`((TextView)findViewById(R.id.OpponentScore_tv)).setText(score);`

`}`

`}`

`}`

`}`

#### 2.初始化laya引擎的时候，和游戏交互，传递给游戏数据

`public void initEngine()`

`{`

`getUser();`

`JSONObject object=new JSONObject();`

`try {`

`object.put("voice",getIntent().getStringExtra("voice"));`

`object.put("time",getIntent().getStringExtra("time"));`

`object.put("model",getIntent().getStringExtra("modle"));`

`} catch (JSONException e) {`

`e.printStackTrace();`

`}`

`mProxy = new RuntimeProxy(this, object.toString(),fromId,myId);`

`mPlugin = new GameEngine(this);`

`mPlugin.game_plugin_set_runtime_proxy(mProxy);`

`mPlugin.game_plugin_set_option("localize","true");`

`mPlugin.game_plugin_set_option("gameUrl", "http://stand.alone.version/index.html");`

`mPlugin.game_plugin_init(3);`

`View gameView = mPlugin.game_plugin_get_view();`

`LinearLayout layout= (LinearLayout) findViewById(R.id.content_layout);`

`layout.addView(gameView);`

`//handler.postDelayed(runnable, 1000);//每两秒执行一次runnable.`

`//this.setContentView(layout);`

`isLoad=true;`

`}`

