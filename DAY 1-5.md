# DAY 1

### 1    Qt简介

1.1    跨平台图形界面引擎

1.2    历史

​		1.2.1  1991 奇趣科技

1.3    优点

​		1.3.1  跨平台

​		1.3.2  接口简单，容易上手

​		1.3.3  一定程度上简化了内存回收

1.4    版本

​		1.4.1  商业版

​		1.4.2  开源版

1.5    成功案例

​		1.5.1  Linux桌面环境 KDE

​		1.5.2  谷歌地图

​		1.5.3  VLC多媒体播放器

### 2    创建第一个Qt程序

2.1    点击创建项目后，选择项目路径以及 给项目起名称

2.2    名称 - 不能有中文 不能有空格

2.3    路径 - 不能有中文路径

2.4    默认创建有窗口类，myWidget，基类有三种选择： QWidget 、QMainWindow、QDialog

2.5    main函数

​		2.5.1  QApplication a 应用程序对象，有且仅有一个

​		2.5.2  myWidget w;实例化窗口对象

​		2.5.3  w.show()调用show函数 显示窗口

​		2.5.4  return a.exec() 让应用程序对象进入消息循环机制中，代码阻塞到当前行

### 3    按钮控件常用API

3.1    创建 QPushButton * btn = new QPushButton

3.2    设置父亲 setParent(this)

3.3    设置文本 setText(“文字”)

3.4    设置位置 move(宽，高)

3.5    重新指定窗口大小 resize

3.6    设置窗口标题 setWindowTitle

3.7    设置窗口固定大小 setFixedSize

### 4    对象树

4.1    当创建的对象在堆区时候，如果指定的父亲是QObject派生下来的类或者QObject子类派生下来的类，可以不用管理释放的操作，将对象会放入到对象树中。

4.2    一定程度上简化了内存回收机制

### 5    Qt中的坐标系

5.1    左上角为 0 ， 0 点

5.2    x以右为正方向

5.3    y以下为正方向

### 6    信号和槽

6.1    连接函数 ：connect

6.2    参数 

​		6.2.1  参数1 信号的发送者

​		6.2.2  参数2 发送的信号（函数地址）

​		6.2.3  参数3 信号的接受者

​		6.2.4  参数4 处理的槽函数 （函数的地址）

6.3    松散耦合

6.4    实现 点击按钮 关闭窗口的案例

6.5    connect(btn , &QPushButton::click , this , &QWidget::close );

### 7    自定义信号和槽

7.1    自定义信号

​		7.1.1  写到 signals下

​		7.1.2  返回 void

​		7.1.3  需要声明，不需要实现

​		7.1.4  可以有参数 ，可以重载

7.2    自定义槽函数

​		7.2.1  返回void

​		7.2.2  需要声明 ，也需要实现

​		7.2.3  可以有参数 ，可以重载

​		7.2.4  写到 public slot下 或者public 或者全局函数

7.3    触发自定义的信号

​		7.3.1  emit 自定义信号

7.4    案例-下课后，老师触发饿了信号，学生响应信号，请客吃饭

### 8    当自定义信号和槽出现重载

8.1    需要利用函数指针 明确指向函数的地址

8.2    void( Teacher:: * tSignal )( QString ) = &Teacher::hungry;

8.3    QString 转成 char *   

​		8.3.1  .ToUtf8() 转为 QByteArray

​		8.3.2  .Data() 转为 Char *

8.4    信号可以连接信号 

8.5    断开信号 disconnect

### 9    拓展

9.1    信号可以连接信号

9.2    一个信号可以连接多个槽函数

9.3    多个信号可以连接同一个槽函数

9.4    信号和槽函数的参数 必须类型一一对应

9.5    信号和槽的参数个数 是不是要一致？信号的参数个数 可以多余槽函数的参数个数

9.6    信号槽可以断开连接 disconnect

### 10   Qt4版本写法

10.1   connect( 信号的发送者， 发送的信号SIGNAL( 信号) ，信号接受者， 槽函数SLOT(槽函数) )

10.2   优点 参数直观

10.3   缺点 编译器不会检测参数类型

### 11   Lambda表达式

11.1   []标识符 匿名函数 

​		11.1.1  = 值传递

​		11.1.2 & 引用传递

11.2   () 参数 

11.3   {} 实现体

11.4   mutable 修饰 值传递变量 ，可以修改拷贝出的数据，改变不了本体

11.5   返回值 []() ->int {}

# DAY 2

### 1    QMainWindow

1.1    菜单栏 最多有一个

​		1.1.1   QMenuBar * bar = MenuBar();

​		1.1.2   setMenuBar( bar ) 

​		1.1.3   QMenu * fileMenu = bar -> addMenu(“文件”)  创建菜单

​		1.1.4   QAction * newAction = fileMenu ->addAction(“新建”); 创建菜单项

​		1.1.5   添加分割线 fileMenu->addSeparator();

1.2    工具栏 可以有多个

​		1.2.1  QToolBar * toolbar = new QToolBar(this);

​		1.2.2  addToolBar( 默认停靠区域， toolbar ); Qt::LeftToolBarArea

​		1.2.3  设置 后期停靠区域，设置浮动，设置移动

​		1.2.4  添加菜单项 或者添加 小控件

1.3    状态栏 最多一个

​		1.3.1  QStatusBar * stBar = statusBar();

​		1.3.2  设置到窗口中 setStatusBar(stBar);

​		1.3.3   stBar->addWidget(label);放左侧信息

​		1.3.4   stBar->addPermanentWidget(label2); 放右侧信息

1.4    铆接部件 浮动窗口 可以多个

​		1.4.1  QDockWidget 

​		1.4.2  addDockWidget( 默认停靠区域，浮动窗口指针)

​		1.4.3  设置后期停靠区域

1.5    设置核心部件 只能一个

​		1.5.1  setCentralWidget(edit);

### 2    资源文件

2.1    将图片文件 拷贝到项目位置下

2.2    右键项目->添加新文件 –> Qt - > Qt recourse File  - >给资源文件起名

2.3    res 生成 res.qrc 

2.4    open in editor 编辑资源

2.5    添加前缀 添加文件

2.6    使用 “ : + 前缀名 + 文件名 ”

### 3    对话框

3.1    分类 ： 

​		3.1.1  模态对话框  不可以对其他窗口进行操作 阻塞

​				3.1.1.1  QDialog dlg(this)

​				3.1.1.2  dlg.exec();

​		3.1.2  非模态对话框 可以对其他窗口进行操作

​				3.1.2.1  防止一闪而过 创建到堆区

​				3.1.2.2  QDialog * dlg = new QDialog(this)

​				3.1.2.3  dlg->show();

​				3.1.2.4  dlg2->setAttribute(Qt::WA_DeleteOnClose); //55号 属性

3.2    标准对话框 -- 消息对话框

​		3.2.1  QMessageBox 静态成员函数 创建对话框

​		3.2.2  错误、信息、提问、警告

​		3.2.3  参数1 父亲 参数2 标题 参数3 显示内容 参数4 按键类型 参数5 默认关联回车按键

​		3.2.4  返回值 也是StandardButton类型，利用返回值判断用户的输入

3.3    其他标准对话框

​		3.3.1  颜色对话框 QColorDialog：：getColor

​		3.3.2  文件对话框 QFileDialog：：getOpenFileName(父亲，标题，默认路径，过滤文件)

​		3.3.3  字体对话框 QFontDialog：：getFont 

### 4    界面布局

4.1    实现登陆窗口

4.2    利用布局方式 给窗口进行美化

4.3    选取 widget 进行布局 ，水平布局、垂直布局、栅格布局

4.4    给用户名、密码、登陆、退出按钮进行布局

4.5    默认窗口和控件之间 有9间隙，可以调整 layoutLeftMargin

4.6    利用弹簧进行布局

### 5    控件

5.1    按钮组

​		5.1.1  QPushButton 常用按钮 

​		5.1.2  QToolButton 工具按钮 用于显示图片，如图想显示文字，修改风格：toolButtonStyle ， 凸起风格autoRaise

​		5.1.3  radioButton 单选按钮，设置默认 ui->rBtnMan->setChecked(true); 

​		5.1.4  checkbox多选按钮，监听状态，2 选中 1 半选 0 未选中

5.2    QListWidget 列表容器

​		5.2.1  QListWidgetItem * item 一行内容

​		5.2.2  ui->listWidget ->addItem ( item )

​		5.2.3  设置居中方式item->setTextAlignment(Qt::AlignHCenter);

​		5.2.4  可以利用addItems一次性添加整个诗内容

5.3    QTreeWidget 树控件

​		5.3.1  设置头 

​				5.3.1.1  ui->treeWidget->setHeaderLabels(QStringList()<< "英雄"<< "英雄介绍");

​		5.3.2  创建根节点

​				5.3.2.1  QTreeWidgetItem * liItem = new QTreeWidgetItem(QStringList()<< "力量");

​		5.3.3  添加根节点 到 树控件上

​				5.3.3.1  ui->treeWidget->addTopLevelItem(liItem);

​		5.3.4  添加子节点

​				5.3.4.1  liItem->addChild(l1);

5.4    QTableWidget 表格控件

​		5.4.1  设置列数 

​				5.4.1.1  ui->tableWidget->setColumnCount(3);

​		5.4.2  设置水平表头

​				5.4.2.1  ui->tableWidget->setHorizontalHeaderLabels(QStringList()<<"姓名"<< "性别"<< "年龄");

​		5.4.3  设置行数 

​				5.4.3.1  ui->tableWidget->setRowCount(5);

​		5.4.4  设置正文

​				5.4.4.1  ui->tableWidget->setItem(0,0, new QTableWidgetItem("亚瑟"));

5.5    其他控件介绍

​		5.5.1  stackedWidget 栈控件

​				5.5.1.1  ui->stackedWidget->setCurrentIndex(1);

​		5.5.2  下拉框

​				5.5.2.1  ui->comboBox->addItem("奔驰");

​		5.5.3  QLabel 显示图片

​				5.5.3.1  ui->lbl_Image->setPixmap(QPixmap(":/Image/butterfly.png"))

​		5.5.4  QLabel显示动图 gif图片

​				5.5.4.1  ui->lbl_movie->setMovie(movie);

​				5.5.4.2  movie->start();

 

# DAY 3

### 1    自定义控件封装

1.1    添加新文件 - Qt – 设计师界面类 (.h .cpp .ui)

1.2    .ui中 设计 QSpinBox和QSlider 两个控件

1.3    Widget中使用自定义控件，拖拽一个Widget，点击提升为，点击添加，点击提升

1.4    实现功能，改变数字，滑动条跟着移动 ，信号槽监听。

1.5    提供 getNum 和 setNum对外接口

1.6    测试接口

### 2    Qt中的事件

2.1    鼠标事件

2.2    鼠标进入事件 enterEvent

2.3    鼠标离开事件 leaveEvent

2.4    鼠标按下  mousePressEvent ( QMouseEvent ev)

2.5    鼠标释放  mouseReleaseEvent

2.6    鼠标移动  mouseMoveEvent

2.7    ev->x() x坐标 ev->y() y坐标

2.8    ev->button() 可以判断所有按键 Qt::LeftButton Qt::RightButton

2.9    ev->buttons()判断组合按键 判断move时候的左右键 结合 & 操作符

2.10   格式化字符串 QString( “ %1 %2 ” ).arg( 111 ).arg(222)

2.11   设置鼠标追踪   setMouseTracking(true);

### 3    定时器1

3.1    利用事件 void timerEvent ( QTimerEvent * ev)

3.2    启动定时器 startTimer( 1000) 毫秒单位

3.3    timerEvent 的返回值是定时器的唯一标示 可以和ev->timerId 做比较

### 4    定时器2

4.1    利用定时器类 QTimer

4.2    创建定时器对象 QTimer * timer = new QTimer(this)

4.3    启动定时器 timer->start(毫秒)

4.4    每隔一定毫秒，发送信号 timeout ,进行监听

4.5    暂停 timer->stop

### 5    event事件

5.1    用途：用于事件的分发

5.2    也可以做拦截操作，不建议

5.3    bool event( QEvent * e); 

5.4    返回值 如果是true 代表用户处理这个事件，不向下分发了

5.5    e->type() == 鼠标按下 …

### 6    事件过滤器 

6.1    在程序将时间分发到事件分发器前，可以利用过滤器做拦截

6.2    步骤

​		6.2.1  1、给控件安装事件过滤器

​		6.2.2  2、重写 eventFilter函数 （obj ， ev）

### 7    QPainter 绘图

7.1    绘图事件 void paintEvent()

7.2    声明一个画家对象 QPainter painter(this) this指定绘图设备

7.3    画线、画圆、画矩形、画文字

7.4    设置画笔 QPen 设置画笔宽度 、风格

7.5    设置画刷 QBrush 设置画刷 风格

### 8    QPainter高级设置

8.1    抗锯齿 效率低

​		8.1.1  painter.setRenderHint(QPainter::Antialiasing);

8.2    对画家进行移动

​		8.2.1  painter.translate(100,0);

​		8.2.2  保存状态 save

​		8.2.3  还原状态 restore

8.3    如果想手动调用绘图事件 利用update

8.4    利用画家画图片 painter.drawPixmap( x，y，QPixmap( 路飞) )

### 9    QPaintDevice绘图设备

9.1    QPixmap QImage QBitmap(黑白色) QPicture QWidget

9.2    QPixmap 对不同平台做了显示的优化

​		9.2.1  QPixmap pix( 300,300)

​		9.2.2  pix.fill( 填充颜色 )

​		9.2.3  利用画家 往pix上画画 QPainter painter( & pix)

​		9.2.4  保存 pix.save( “路径”)

9.3    Qimage 可以对像素进行访问

​		9.3.1  使用和QPixmap差不多 QImage img(300,300,**QImage::Format_RGB32**);

​		9.3.2  其他流程和QPixmap一样

​		9.3.3  可以对像素进行修改 img.setPixel(i,j,value);

9.4    QPicture  记录和重现 绘图指令

​		9.4.1  QPicture pic

​		9.4.2  painter.begin(&pic);

​		9.4.3  保存 pic.save( 任意后缀名 )

​		9.4.4  重现 利用画家可以重现painter.drawPicture(0,0,pic);

### 10   QFile 对文件进行读写操作

10.1   QFile进行读写操作

10.2   QFile file( path 文件路径)

10.3   读

​		10.3.1 file.open(打开方式) QIODevice::readOnly

​		10.3.2 全部读取 file.readAll()  按行读 file.readLine() atend()判断是否读到文件尾

​		10.3.3 默认支持编码格式 utf-8

​		10.3.4 利用编码格式类 指定格式 QTextCodeC 

​		10.3.5 QTextCodec * codec = QTextCodec::codecForName("gbk");

​		10.3.6 //ui->textEdit->setText( codec->toUnicode(array) );

​		10.3.7 文件对象关闭 close

10.4   写

​		10.4.1 file.open( QIODevice::writeOnly / Append)

​		10.4.2 file.write(内容)

​		10.4.3 file.close 关闭

### 11   QFileInfo 读取文件信息

11.1   QFileInfo info(路径)

11.2   qDebug() << "大小：" << info.size() << " 后缀名：" << **info.suffix()** << " 文件名称："<<info.fileName() << " 文件路径："<< info.filePath();

11.3       qDebug() << "创建日期：" << info.created().toString("yyyy/MM/dd hh:mm:ss");

11.4       qDebug() << "最后修改日期："<<info.lastModified().toString("yyyy-MM-dd hh:mm:ss");

 

# DAY 4

### 1    项目简介

### 2    创建项目、添加项目资源

### 3    项目 基本配置

3.1    设置背景图标

3.2    设置固定大小

3.3    设置项目标题

3.4    设置背景

3.5    背景标题

3.6    开始菜单 – 退出功能

### 4    创建开始按钮

4.1    封装自定义按钮 MyPushButton

4.2    构造函数 （ 默认显示图片， 按下后显示的图片）

4.3    测试开始按钮

4.4    开始制作特效

4.5    zoom1 向下跳 

4.6    zoom2 向上跳

### 5    创建选择关卡场景

5.1    点击开始按钮后 延时进入到 选择关卡场景

5.2    配置选择关卡场景（图标、标题、大小）

5.3    设置背景图片、设置标题图片

5.4    创建返回按钮

### 6    选择关卡的返回按钮特效制作

6.1    点击后切换另一个图片

6.2    重写 void mousePressEvent

6.3    重写 void mouseReleaseEvent

### 7    开始场景与选择关卡场景的切换

7.1    点击选择关卡场景的返回按钮，发送一个自定义信号

7.2    在主场景中监听这个信号，并且当触发信号后，重新显示主场景，隐藏掉选择关卡的场景

### 8    选择关卡中的 按钮创建

8.1    利用一个for循环将所有按钮布置到场景中

8.2    在按钮上面 设置一个QLabel显示关卡数

​		8.2.1  QLabel 设置 大小、显示文字、对齐方式、鼠标穿透

8.3    给每个按钮 监听点击事件

### 9    翻金币场景创建

9.1    点击选择关卡按钮后，进入到翻金币游戏场景

9.2    配置翻金币游戏场景 设置标题、图标、大小、设置背景

9.3    实现返回按钮，可以返回到上一个场景（选关场景）

9.4    实现三个场景之间的切换

### 10   实现显示关卡标签

10.1   在左下角显示玩家具体的关卡标签

10.2   QLabel创建设置 大小和位置label->setGeometry(30, this->height() - 50,120, 50);

10.3   QFont font 设置字体以及字号

10.4   给QLabel设置字体 setFont（font）

 
