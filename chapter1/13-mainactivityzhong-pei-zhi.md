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

#### 3.定时器时间到了，通知游戏

 `Runnable runnable=new Runnable() {`

`        @Override`

`        public void run() {`

`            try{`

`                //此处做定时器操作`

`                i++;`

`                ((TextView)findViewById(R.id.timer_tv)).setText(""+i+"S");`

`                if(i==time){`

`                    //时间到了，发送结束命令`

`                    Log.e("message", "Logout SendMessageToPlatform = "+"end");`

`                    ConchJNI.RunJS("onRecvMessage('{\"cmd\":\"end\"}')");`

`                }`

`                handler.postDelayed(this, 1000);`

`            }catch (Exception e){`

``

`            }`

``

        }

    };

#### 4.退出游戏，杀死进程

`findViewById(R.id.exit_iv).setOnClickListener(new View.OnClickListener() {`

`            @Override`

`            public void onClick(View view) {`

`                finish();`

`                new Handler().postDelayed(new Runnable() {`

`                    @Override`

`                    public void run() {`

`                        int pid = android.os.Process.myPid();`

`                        Log.e("message", "Logout SendMessageToPlatform = "+pid);`

`                        android.os.Process.killProcess(pid);`

`                    }`

`                }, 100);`

`            }`

`        });`



