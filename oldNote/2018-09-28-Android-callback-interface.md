---
layout: post
title: Android回调接口
categories: [Android]
description: Android回调接口学习笔记
keywords: callback, interface
---

# Android回调接口

Andorid的button的setOnClickListener绝对是一个经典的接口回调例子，大家都经常这样写对吧，然后我们点了这个button就可以执行我们在onClick里面的代码了。

```java
bt.setOnClickListener(new View.OnClickListener() {
          @Override
            public void onClick(View v) {
               //执行代码...
            }
        });
```

## 1.定义一个接口，接口里面写执行的方法

```java
  //1 定义接口
    public interface myCallBack {
        void setLog(String s);
    }
```

## 2.需要引用的地方持有该接口的引用

```java
//2 持有接口引用
    private  myCallBack mMyCallBack;
```

## 3.持有该接口的地方生成该接口的set方法

```java
   //3 set方法
    public  void setMyCallBack(myCallBack myCallBack) {
        this.mMyCallBack = myCallBack;
    }
```

## 4.调用时实现接口（调用后不立即执行）

```java
activityB.setMyCallBack(new ActivityB.myCallBack() {
    @Override
    public void setLog(String s) {
        Log.v("Az", "tv_1 onClick" + s);
    }
});

```

## 5.用某个方法xxx来为接口设置接口值（设置值后才会执行）

```java
  public void startB(){
        mMyCallBack.setLog("activityB");
    }

```

## 6.调用XXX方法设置接口值

这就是面向接口编程的要义-接口变量存放实现该接口的类的对象的引用，从而接口变量可以调用接口方法，该接口方法即为被实现的接口的方法。 

MainAvtivity.java

```java
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    private ClassB classB;
    private ClassC classC;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initView();
    }

    private void initView() {
        TextView tv_1 = findViewById(R.id.tv_1);
        TextView tv_2 = findViewById(R.id.tv_2);
        tv_1.setOnClickListener(this);
        tv_2.setOnClickListener(this);
        classB = new ClassB();
        classC = new ClassC();
                //调用 自己实现接口中的方法
        classB.setMyCallBack(new ClassB.myCallBack() {
            @Override
            public void setLog(String s) {
                //自己实现接口中的方法
                Log.v("Az", "tv_1-->" + s);
            }
        });
        classC.setMyCallBack2(new ClassC.myCallBack2() {
            @Override
            public void setLog(String s) {
                Log.v("Az", "tv_2-->" + s);
            }
        });
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.tv_1:
                Log.v("Az", "tv_1 onClick");
                classB.startB("Hello World!");//调用该方法为接口设值，然后就会执行接口中的方法
                break;
            case R.id.tv_2:
                Log.v("Az", "tv_2 onClick");
                classC.startC();
                break;
        }
    }
}
```

ClassB.java

```java
public class ClassB {
    //2 持有接口引用
    private  myCallBack mMyCallBack;

    //1 定义接口
    public interface myCallBack {
        void setLog(String s);
    }

    //3 set方法
    public  void setMyCallBack(myCallBack myCallBack) {
        this.mMyCallBack = myCallBack;
    }
    // public 方法给接口设值
    public void startB(String s){
//        mMyCallBack.setLog("Hello World!");
        mMyCallBack.setLog(s);
    }

}
```

ClassC.java

```java
public class ClassC {
    //2 持有接口引用
    private  myCallBack2 mMyCallBack2;


    //1 定义接口
    public interface myCallBack2 {
        void setLog(String s);
    }

    //3 set方法
    public  void setMyCallBack2(myCallBack2 myCallBack2) {
        this.mMyCallBack2 = myCallBack2;
    }
// public 方法给接口设值
    public void startC(){
        mMyCallBack2.setLog("Hello Android!");
    }
}
```

activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/tv_1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Hello World!" />

    <Button
        android:id="@+id/tv_2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Hello Android" />

</LinearLayout>
```

有点乱，自己也不是很懂，不知道是不是这样的，先记下来好了。