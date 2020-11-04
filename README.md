生命周期，数据传递，优缺点，使用场景。遇到过bug并解决
Activity生命周期:
            OnCreate():设置布局以及进行初始化操作
            OnStart():  可见
            OnResume():得到焦点
            onRestart():当Activity没有被销毁的时候重新调用这个Activity.
            onPause():失去焦点
            onStop():不可见
            onDestory():被销毁.·

Fragment生命周期:
            onAttach() :Fragment关联Activity
            onCreate():
            onCreateView():当activity要得到fragment的layout时,调用 此方法,Fragment在其中创建自己的layout(界面)
            onActivityCreated():当activity的onCreated()方法返回后调用此方法
            onStart():界面可见
            onResume():获得焦点
            onPause():失去焦点
            onStop():界面不可见
            onDestroyView():当fragment中的视图被移除的时候，调用这个方法
            onDetach():当fragment和activity分离的时候，调用这个方法。 

数据传递:
            Activity和Fragment之间的数据传递可以使用Intent(意图),传递数据.
            Intent分为隐式意图和显示意图:
            显示意图场景：应用程序内部跳转时，效率高
            默认开启方式:用startActivity方法跳转
            隐式意图场景：开启另外一个应用程序页面时，效率低，需要去遍历所有应用程序的意图过滤器
            默认开启方式:被打开的activity A配置意图过滤器

区别:

Fragment用来描述一些行为或一部分用户界面在一个Activity中，你可以合并多个fragment在一个单独的activity中建立多个UI面板，同时重用fragment在多个activity中.你可以认为fragment作为一个activity中的一节模块 ，fragment有自己的生命周期，接收自己的输入事件，你可以添加或移除从运行中的activity.

遇到的BUG,以及解决方案:

ANR异常:Application not response 应用程序无响应
                产生原因：在主线程做了耗时的操作
    解决方法:引入Handler消息机制:
                子线程不能修改UI界面，修改UI界面需要在主线程完成，这样引入了handler消息机制 .
            代码步骤:
                    1.在主线程里，初始化Handler---------------------->Handler handler = new Handler
                    2.在子线程里初始化Message对象--------------->Message msg = Message.obtain();
                    3.设置msg的标识以及需要传递的值------------->msg.what=?  设置标识            
                                                                                                      msg.obj=? 设置值
                    4.利用Handler发送消息------------------------>handler.sendMessage(msg);
                    5.重写Handler里的handleMessage方法------->public void handleMessage(Message msg) {...}

Activity横竖屏切换问题
            产生原因：在activity横竖屏切换的时候默认是销毁当前的activity，然后重新初始化activity
            解决办法:
                        清单文件定死一个朝向--------------->android:screenOrientation="portrait"
                        配置configChanges，指定某些情况发生了不影响activity---->android:configChanges="keyboardHidden|screenSize|orientation"

