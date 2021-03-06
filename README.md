# py_exceltools
基于openpyxl的excel转换工具。支持xlsx文件转换为lua、xml、json等配置文件。
由于解析库从xlrd更换为openpyxl，不再支持xls文件的转换。可以导出数组、map两种类型excel。

关于openpyxl库：https://pypi.python.org/pypi/openpyxl。

此工具兼容python2和python3。


## 安装

linux安装  

    apt-get install python-pip
    pip install openpyxl
    git clone https://github.com/changnet/py_exceltools.git
    git git submodule update --init --recursive

ps:
```
"Cannot fetch index base URL http://pypi.python.org/simple/"  
尝试：pip install openpyxl --index-url=https://pypi.python.org/simple/
```

win安装

    安装python(同时安装pip并添加到Path):https://www.python.org/downloads/windows/
    安装openpyxl,在cmd中运行:pip install openpyxl
    git clone https://github.com/changnet/py_exceltools.git
    git git submodule update --init --recursive

# 使用
    lancher.bat(win)和lancher.sh(linux)为对应运行脚本。
    当前配置了用于参考的参数来转换example.xlsx，可在server、client文件夹查看生成配置效果。

    参数：
    --input   ：需要转换的excel文件所在目录
    --srv     : 服务端配置文件输出目录
    --clt     : 客户端配置文件输出目录
    --timeout : 需要转换的excel文件最后更新时间距当前时间秒数。-1转换所有
    --suffix  ：excel文件后缀，通常为.xlsx 
    --swriter : 服务端配置文件转换器，可以指定为lua、json、xml
    --cwriter : 客户端配置文件转换器，可以指定为lua、json、xml

    注：对于client和server，如果未配置输出目录或转换器，则不会导出。

# 数据类型
    支持int(int64)、number(float)、string、json、lua

# 打包exe
部署时，可以将python打包成exe。建议使用pyinstaller。截止发版时(2017-07-29),由于最新的
pyinstaller3.2.1尚不支持python3.6.1，建议使用python 3.5。

    pip install pyinstaller
    pyinstaller -F -c reader.py

# 建议
* 文件命名支持 mmmnnn.xlsx的方式。mmm可以是任意字符，nnn只能是数字和字母，导出的配置以
nnn做为前缀，当然也可以只用nnn.xlsx。例如:Y_样本_example.xlsx，方便管理文件
* 在string中无法直接使用换行等特殊称号。请用\n等转义字符替代。
* 设置表结构时，数据尽量偏平化。例如一个玩家身上有8种装备，不应该配8个表，而是在装备表中加一个字段pos
* 由于xml并不存在数组等结构，不建议使用。
* 工具会检测server和client标识。如果不存在，则不导出些表。方便策划做备注

# 二次开发
如果你要新增加导出的格式，则参考writer.py中json、xml、lua的实现即可
