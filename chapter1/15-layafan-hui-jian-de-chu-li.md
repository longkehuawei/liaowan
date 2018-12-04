#### **1.GameEngine 类中，把引擎拦截键盘的设置为false**

#### 在**game\_plugin\_init\(\)方法中**

**mLayaGameEngine.setInterceptKey\(false\);**

---

**2.在MainActivity中，禁止掉返回键**

`@Override`

`    public boolean onKeyDown(int keyCode, KeyEvent event)`

`    {`

`        if (keyCode == KeyEvent.KEYCODE_BACK) {`

`            return true;`

`        }`

``

`        return super.onKeyDown(keyCode, event);`

`    }`



    



