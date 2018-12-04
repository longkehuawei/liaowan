# 添加项目依赖

#### 1.项目根目录下build.gradle

    ` classpath 'com.qihoo360.replugin:replugin-plugin-gradle:2.2.4'`

![](/assets/TIM截图20180828175205.png)

#### 2.app 目录下build.gradle

`compile 'com.qihoo360.replugin:replugin-plugin-lib:2.2.4'`

`apply plugin: 'replugin-plugin-gradle'`

```
compile 'org.greenrobot:eventbus:3.0.0'
compile 'com.github.bumptech.glide:glide:3.7.0'
```

![](/assets/TIM截图20180828175350.png)

