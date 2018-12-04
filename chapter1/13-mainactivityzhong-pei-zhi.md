# MainActivity中配置

#### 1.处理平台消息

/\*\*

     \* 处理平台消息

     \*/

   ` private class GameMessageBroadcastReceiver extends BroadcastReceiver {`

`        @Override`

`        public void onReceive(Context context, Intent intent) {`

`            //游戏发送过来的消息`

`            if(intent.getAction().equals(FROM_GAME_ACTION)){`

`                if(intent.getStringExtra("type").equals("finish")){`

`                    finish();`

`                    new Handler().postDelayed(new Runnable() {`

`                        @Override`

`                        public void run() {`

`                            int pid = android.os.Process.myPid();`

`                            Log.e("message", "Logout SendMessageToPlatform = "+pid);`

`                            android.os.Process.killProcess(pid);`

`                        }`

`                    }, 100);`

`                }else{`

`                    String score= intent.getStringExtra("score");`

`                    ((TextView)findViewById(R.id.OpponentScore_tv)).setText(score);`

`                }`

`            }`

`        }`

`    }`

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

