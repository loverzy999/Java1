JAVA实验报告
========
大数据181刘仁轩2018310378

实验目的
=======
分析学生选课系统

使用GUI窗体及其组件设计窗体界面

完成学生选课过程业务逻辑编程

基于文件保存并读取数据

处理异常

实验要求
====
(定义学生的属性，设置为人员(学号、姓名、性别、密码、年龄)，学生(学号、姓名、性别、密码、年龄、所选科目)，课程(编号、名称、上课地点、上课时间、学分、授课教师)
设计GUI窗体，支持学生注册、学生选课、学生退课、打印学生信息选课列表等操作.基于事件模型对业务逻辑编程，实现在界面上支持的操作.针对操作过程中可能会出现的各种异常，做异常处理.基于输入/输出编程，支持学生、课程、教师等数据的读写操作.

实验过程
====
以学生端的编写为例：

编写从文件读取学生名列表的方法：

根据读取学生名列表文件地址，新建一个文件对象文件，根据文件新建一个FileInputStream对象，以此创建一个ObjectInputStream对象ObjectInputStream对象ObjectInputStream，创建一个字符串列表，用于存放通过ObjectInputStream的readObject方法读取到的String列表，关闭ObjectInputStream对象，返回存有读取到String列表的String列表。

编写从文件读取学生对象列表的方法:

创建一个学生类的列表用于储存从文件中读取的学生类列表，根据文件地址新建一个文件对象文件，根据文件新建一个FileInputStream对象，以此创建一个ObjectInputStream对象objectInputStream，用readObject方法将文件中的学生类列表读出，赋值给先前创建好的学生类列表，返回这个列表。

编写将学生名列表写入文件的方法：

根据文件路径新建一个FileOutputStream对象，根据这个对象新建一个ObjectOutputStream对象利用writeObject将学生名列表存入文件，关闭ObjectOutputStream对象。

编写将学生类列表写入文件：

根据文件路径新建一个FileOutputStream对象，根据这个对象新建一个ObjectOutputStream对象利用writeObject将学生名列表存入文件，关闭ObjectOutputStream对象。

编写GUI窗体：

编写登陆窗口:

创建JFrame对象，设置FlowLayout布局，设置可见，设置位置大小；创建一个Container对象，存放各种组件。创建一个“用户名：”的JLabel，随后创建一个JTextField对象让用户输入用户名；创建一个“密码：”的JLabel，随后创建一个JPasswordField让用户输入密码；创建两个JButton，一个为登陆，一个为注册.安装创建的顺序用添加方法加入容器对象。

编写注册窗口:

创建JFrame对象，设置FlowLayout布局，设置可见，设置位置大小；建一个“用户名：”的JLabel，随后创建一个JTextField对象让用户输入用户名；创建一个“密码：”的JLabel，随后创建一个JPasswordField让用户输入密码；创建一个JTextField对象让用户输入学号；创建一个“所选课程：”的JLabel，创建四个多选项王老师-物理，李老师-化学，利老师-生物，真老师-物理；设置一个为确定的按钮用于提交注册信息。

编写学生操作窗口：

创建JFrame对象，设置FlowLayout布局，设置可见，设置位置大小；设置四个按钮，分别为“学生选课信息”、“学生退课信息”、“修改学生信息”、“打印学生选课信息”。

编写退课/选课窗口：

创建JFrame对象，设置FlowLayout布局，设置可见，设置位置大小；设置四个单选项，王老师-物理，李老师-化学，利老师-生物，真老师-物理；，设置一个确定按钮用于提交。

业务逻辑：
=====
首先从文件中读取出学生姓名的列表和学生类的列表，当用户点击注册后弹出注册界面，当用户输入完毕信息，点击确认后，根据用户在输入框和选择项的选择创建一个新的学生类，并添加学生姓名到学生姓名列表，且添加学生类到学生类的列表中然后写入文件.针对所选课程的设置，使用了if进行判断，判断用户选择的课程及老师，当用户只选择了王老师-物理则在此创建学生类，所选科目及老师为王老师-物理；当用户只选择了李老师-化学则在此创建学生类，所选科目为李老师-化学；根据用户输入的用户名，在学生名的列表中进行查找索引，因为在设计时学生姓名和学生类是一同添加到各个列表的，所以可以根据用户名在学生姓名的列表索引找的学生类中对应的学生.当用户输入的密码与其对应学生类中的密码对应是登陆成功，弹出学生操作界面，否侧提示用户“用户名或密码不正确！”...当用户点击选课/退课按钮后，弹出选课/退课界面，根据用户所选课程，当用户点击确定后利用学生类中的加载项/删除方法对课程进行选课/退课操作，并弹出提示框告知用户选课/退课成功。当用户点击打印信息按钮时，调用学生类的Show方法，通过提示框告知用户的打印信息结果.

核心代码
====
标题窗口

        JLabel titleJL = new JLabel("学生选课系统");
        Font font = new Font("微软雅黑", 1, 15);
        titleJL.setFont(font);
        titleJL.setLayout(null);
        titleJL.setBounds(250, 10, 100, 20);

添加学生信息
        
        jbAdd.addMouseListener(new MouseAdapter(){
            JTextField nameJTF = null;
            JTextField numJTF = null;
            JTextField classJTF = null;
            JTextField professionalJTF = null;
            @Override
            public void mouseClicked(MouseEvent e) {
                final JFrame addJF = new JFrame();
                addJF.setSize(300, 400);
                addJF.setBackground(Color.gray);
                addJF.setLocationRelativeTo(null);
                addJF.setVisible(true);
                addJF.setLayout(new FlowLayout());
                JLabel numJL = new JLabel("学号：");
                numJTF = new JTextField(20);
                JLabel nameJL = new JLabel("姓名：");
                nameJTF = new JTextField(20);
                JLabel classJL = new JLabel("班级：");
                classJTF = new JTextField(20);
                JLabel professionalJL = new JLabel("选课：");
                professionalJTF = new JTextField(20);
                JLabel l2=new JLabel("--");
                final JComboBox<String> c1 = new JComboBox<String>();//创建一个下拉列表框c1
                c1.addItem("----");
                c1.addItem("王老师-物理");       // 创建4个下拉选项
                c1.addItem("李老师-化学");
                c1.addItem("利老师-生物");
                c1.addItem("真老师-物理");
                JPanel l3=new JPanel();
                l3.add(l2);
                l3.add(c1);
                //addJF.dispose();//销毁子窗口
                addJF.add(numJL);
                addJF.add(numJTF);
                addJF.add(nameJL);
                addJF.add(nameJTF);
                addJF.add(classJL);
                addJF.add(classJTF);
              //  addJF.add(professionalJL);
              //  addJF.add(professionalJTF);
                addJF.add(l3);
                JButton addJB = new JButton("添加");
                addJF.add(addJB);
                addJB.addMouseListener(new MouseAdapter() {
                    @Override
                    public void mouseClicked(MouseEvent e) {
                        Integer snumAddI = new Integer(numJTF.getText().toString());
                        int snumAdd = snumAddI;
                        String snameAdd = nameJTF.getText();
                        String sclassAdd = classJTF.getText();
                        String sprofessionalAdd = (String)c1.getSelectedItem();
                       if(snumAdd <0 | snameAdd == null | sclassAdd == "" | sprofessionalAdd == "") {
                            JFrame tipJF = new JFrame("提示");
                            tipJF.setVisible(true);
                            tipJF.setSize(200,100);
                            tipJF.setLocationRelativeTo(null);
                            JLabel tipJL = new JLabel("请填入了所有的信息之后再点击提交");
                            tipJF.add(tipJL);
                        }else {
                            stu = new Student();
                            stu.addStuInfo(snumAdd, snameAdd, sclassAdd, sprofessionalAdd);
                            addJF.dispose();
                            JFrame addSuccessfulJF = new JFrame("提示");
                            addSuccessfulJF.setLocationRelativeTo(null);
                            addSuccessfulJF.setSize(260, 100);
                            addSuccessfulJF.setVisible(true);
                            addSuccessfulJF.setLayout(new FlowLayout());
                            JLabel SuccessfulJL = new JLabel("添加学生信息成功！");
                            addSuccessfulJF.add(SuccessfulJL);
                        }
                    }

                });
            }
        });

修改学生信息

        public void modifyStuInfo(Student stu, int sNum, String sName, String sClass, String sProfessional) {
        int i=0;
       // Student stu=new Student();
        for(i=0;i<liststudent.size();i++){
            if( liststudent.get(i).stuNum==sNum){
                 liststudent.get(i).stuNum=sNum;
                liststudent.get(i).stuName=sName;
                liststudent.get(i).stuClass=sClass;
                liststudent.get(i).stuProfessional=sProfessional;
            //s    liststudent.get(i)

            }
        }
    }

    public List<Student> queryAllStuInfo() {
        return liststudent;
    }

实验感想
=====
通过这次实验，我综合运用了课上学到的知识，对所学的JAVA知识有了进一步的了解，更加深刻了解了GUI设计知识，熟练掌握了事件模型的运用方法。并运用了IO的读写方法，深刻的体会到了可序列化接口的使用方法，加强了我对于使用GUI窗体及其组件设计窗体界面、完成实际问题业务逻辑编程、基于文件保存并读取数据和处理异常的知识，也对我以后的学习起到了引导作用。
