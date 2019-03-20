# Spinner 使用

### 设置下拉列表位置

下拉框遮挡Spinner显示框，解决方法：
android:spinnerMode=”dropdown” 
该行代码就是设置下拉框弹出位置的属性，分为：dropdown（显示框下面显示）和dialog（下拉列表弹出形式）。 
有的手机即使这样设置后取到了一定的效果。但是会出现一种情况：下拉框遮挡住了Spinner的显示框，这是因为有一个属性： 
android:overlapAnchor=”false” 。 
这个属性默认是true。改为false即可。

### 设置 adapter
```
      //资源转[]
        val datas = arrayOf("Java", "Python", "Golang", "Kotlin")
        val adapter = ArrayAdapter<String>(this, android.R.layout.simple_spinner_item,datas)

        
        // adapter 或者将可选内容与ArrayAdapter连接起来
        // 第一个参数为Context对象
        // 第二个参数为要显示的数据源,也就是在string.xml配置的数组列表
        // 第三个参数为设置Spinner的样式
        val adapter = ArrayAdapter.createFromResource(this, R.array.countries, android.R.layout.simple_spinner_item)

        // 设置Spinner中每一项的样式
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item)

        // 设置Spinner数据来源适配器 ，还可以定义 adapter 
        spinner.setAdapter(adapter)

        // 使用内部类形式来实现事件监听
        spinner.setOnItemSelectedListener(object : AdapterView.OnItemSelectedListener {
            override fun onItemSelected(
                parent: AdapterView<*>, view: View,
                position: Int, id: Long
            ) {
                /*
                 * 第一个参数parent是你当前所操作的Spinner，可根据parent.getId()与R.id.
                 * currentSpinner是否相等，来判断是否你当前操作的Spinner,一般在onItemSelected
                 * 方法中用switch语句来解决多个Spinner问题。
                 * 第二个参数view一般不用到；
                 * 第三个参数position表示下拉中选中的选项位置，自上而下从0开始；
                 * 第四个参数id表示的意义与第三个参数相同。
                 */

                //对选中项进行显示
                //Toast用于临时信息的显示
                //第一个参数是上下文环境，可用this；
                //第二个参数是要显示的字符串；
                //第三个参数是显示的时间长短；
                val str = parent.getItemAtPosition(position).toString()
                Toast.makeText(applicationContext, "您选择的国家是：$str", Toast.LENGTH_LONG)
                    .show()
            }

            override fun onNothingSelected(parent: AdapterView<*>) {

            }
        })
        
  ```
  
  github 上有个 NiceSpinner ，自定义的Spinner
  
