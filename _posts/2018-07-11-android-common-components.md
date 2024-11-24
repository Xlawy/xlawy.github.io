---
title: 【Android】常用控件
date: 2018-07-11 10:25 +0800
categories: [Android]
tags: [android, gui]
---
* 为了在代码中可以用变量表示控件，需要设置id：android:id="@+id/btDial"
* 通过id获取控件到变量中：findViewById(R.id.btDial)

## 线性布局LinearLayout
* 排列方向：android:orientation（属性都是android:开头）
* 控件添加在布局标签内：

```xml
<LinearLayout 属性...>
    <TextView 属性... />
    <Button 属性... />
</LinearLayout>
```

## 标签TextView
* 长宽：layout_width、layout_height属性，wrap_content：包裹内容，自动调整大小；match_parent：与父容器一样长/宽
* 内容：text属性，不要硬编码，字符串资源放在string.xml，引用字符串：@string/字符串名
* 将字符串提取到string.xml的快捷键：选中字符串按Alt+Enter
* 文字大小：android:textSize，单位选sp

## 输入框：EditText
* 提示文字：hint属性
* 获取输入的文字：getText().toString()
* inputType属性指定输入类型（文字、数字、密码、日期等），XML文件中静态设置值与代码中动态设置值的对应：<https://blog.csdn.net/ysh06201418/article/details/71123273>

## 按钮：Button
* 右对齐：android:layout_gravity="right"
* 设置按钮点击事件的4种方法：

(1) 内部类

在Activity中声明内部类：

```java
private class MyClick implements View.OnClickListener {
    @Override
    public void onClick(View view) {
        // 事件代码
    }
}
```

设置点击事件：

```java
button.setOnClickListener(new MyClick());
```

(2) （推荐）虚拟匿名类

设置点击事件：

```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        // 事件代码
    }
});
```

如果不在其他地方使用，也可以省略变量：

```java
findViewById(R.id.xx).setOnClickListener(new View.OnClickListener() {...});
```

(3) （推荐）onClick属性：android:onClick="call"，事件代码写入call(View view)函数，使用这种方式不需为按钮设置id和声明变量

(4) 强行介入：直接让Activity实现View.OnClickListener接口并重写onClick()方法，并在onClick(view)中用switch (view.getId())，设置点击事件：

```java
button.setOnClickListener(this);
```

这种方法同时为一组按钮设置点击事件（如计算器应用）。

## 下拉列表Spinner
* 设置列表项目的两种方法：

(1) string-array资源+entries属性

string.xml中写string-array：

```xml
<string-array name="comboItems">
    <item>下拉列表项目1</item>
    <item>下拉列表项目2</item>
    <item>下拉列表项目3</item>
</string-array>
```

activity_main.xml中设置Spinner空间的属性：

```xml
android:entries="@array/comboItems"
```

(2) 适配器Adapter

Activity代码中：

```java
ArrayAdapter<String> adapter = new ArrayAdapter<>(this, R.layout.support_simple_spinner_dropdown_item, newComboItems);
spinner1.setAdapter(adapter);
```

注意：ArrayAdapter构造器的第二个参数一定要写R.layout.support_simple_spinner_dropdown_item而不能是R.layout.activity_main，否则执行setAdapter(adapter)时会产生空指针异常！

```
java.lang.IllegalStateException: ArrayAdapter requires the resource ID to be a TextView
```

使用这种方法也可以在代码中动态设置列表项目

注意：若没有添加v7兼容包，即继承自Activity而不是AppCompatActivity则不能使用R.layout.support_simple_spinner_dropdown_item，否则会报错：

```
java.lang.RuntimeException: Failed to resolve attribute at index 6
```

应改为android.R.layout.simple_spinner_item或android.R.layout.simple_spinner_dropdown_item

* 设置项目选择事件：

```java
spinner1.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
    @Override
    public void onItemSelected(AdapterView<?> adapterView, View view, int i, long l) {
        Toast.makeText(MainActivity.this,
                "你选择的是第" + (i + 1) + "项：" + adapterView.getItemAtPosition(i),
                Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onNothingSelected(AdapterView<?> adapterView) {

    }
});
```

注意是setOnItemSelectedListener而不能是setOnClickListener或setOnItemClickListener，否则会产生异常（和两个方法不能用）

## 开关Switch
* 设置点击事件：

```java
switch1.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(CompoundButton compoundButton, boolean b) {

    }
});
```

参数b表示是否打开

## 列表ListView
* 设置适配器：

```java
lvResult.setAdapter(new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, persons));
```

其中ArrayAdapter:

```java
public ArrayAdapter(Context context, int resource, List<T> objects);
```

* 设置点击事件：

```java
lvResult.setOnItemClickListener(new AdapterView.OnItemClickListener() {
    @Override
    public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
        Toast.makeText(MainActivity.this, "你点击了第" + position + "项：\n"
                + parent.getItemAtPosition(position), Toast.LENGTH_SHORT).show();
    }
});
```

* 屏幕外的item无法通过getChildAt方法获取到，只能通过adapter获取 参考：<https://www.cnblogs.com/linjzong/p/3494090.html>

* 如果ListView是最后一个控件则会自动填满剩余空间，并自带滚动功能，但如果下面还有其他控件则这些控件不会被显示；如果将ListView嵌套于ScrollView则只有一项的高度
参考：<https://www.jianshu.com/p/5f198f8a0977>

## [WebView]({% post_url 2020-02-17-android-webview %})
