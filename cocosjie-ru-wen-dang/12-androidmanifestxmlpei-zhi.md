# AndroidManifest.xml配置

#### 1.游戏插件名字和插件版本号

这个一定要配置唯一名字，版本号是整数，可以从1开始，用来做平台内游戏升级用的

    `  
    <
    meta-data

`android:name="com.qihoo360.plugin.name"`

`android:value="laya"/>`

`<!--插件版本-->`

`<meta-data`

`android:name="com.qihoo360.plugin.version.ver"`

`android:value="102"/>`

#### ![](blob:file:///82032acd-f5f2-4a2b-bc05-0c10632efa72)

---

#### 2.配置进程名字

`<application`

`android:allowBackup="true"`

`android:process=":lieniao"`

`android:icon="@mipmap/ic_launcher"`

`android:label="@string/app_name">`

