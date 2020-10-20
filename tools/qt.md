# QT

QT是一个跨平台的 C++开发库，主要用来开发图形用户界面（Graphical User Interface，GUI）程序，当然也可以开发不带界面的命令行（Command User Interface，CUI）程序。



## 项目文件

- .pro文件    存储项目设置的文件
- main.cpp  实现main函数的程序文件
- .ui文件        一个XML格式存储的窗体上的元件及其布局的文件
- widget.h     所设计的窗体类的头文件



## 信号与槽

信号与槽（Signal & Slot）是 [Qt](http://c.biancheng.net/qt/) 编程的基础，也是 Qt 的一大创新。因为有了信号与槽的编程机制，在 Qt 中处理界面各个组件的交互操作时变得更加直观和简单。

信号（Signal）就是在特定情况下被发射的事件，例如PushButton 最常见的信号就是鼠标单击时发射的 clicked() 信号，一个 ComboBox 最常见的信号是选择的列表项变化时发射的 CurrentIndexChanged() 信号。

槽（Slot）就是对信号响应的函数。槽就是一个函数，与一般的[C++](http://c.biancheng.net/cplus/)函数是一样的，可以定义在类的任何部分（public、private 或 protected），可以具有任何参数，也可以被直接调用。槽函数与一般的函数不同的是：槽函数可以与一个信号关联，当信号被发射时，关联的槽函数被自动执行。

信号与槽关联是用 QObject::connect() 函数实现的，其基本格式是：

> QObject::connect(sender, SIGNAL(signal()), receiver, SLOT(slot()));



## 可能出现的问题

- QT类库以模块的形式组织各种功能的类，根据项目涉及的功能需求，在项目中添加适当的类库模块支持。例如，在项目中使用到数据库操作就需要用到sql模块，**需要在pro文件中增加如下一行**

  > Qt += sql

  ​		

- cannot find lGL错误

  > sudo apt install libgl1-mesa-dev

