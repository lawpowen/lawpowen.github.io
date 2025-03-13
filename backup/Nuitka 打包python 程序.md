转载自 https://www.cnblogs.com/smallbike/p/nuitka.html#%E6%89%93%E5%8C%85%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4%E4%BD%BF%E7%94%A8nuitka---help%E5%8F%AF%E6%9F%A5%E7%9C%8B%E6%89%80%E6%9C%89%E5%91%BD%E4%BB%A4
 
### Windows
```
pip install ordered-set # 加速编译
pip install nuitka
pip install zstandard # onefile时压缩文件
# 打包命令
python -m nuitka --mingw64 --standalone --output-dir=out --show-progress --onefile --plugin-enable=upx --enable-plugin=tk-inter --windows-disable-console pack_seckill.py
```
### Linux
```
    pip install ordered-set # 加速编译
    pip install nuitka
    pip install zstandard # onefile时压缩文件
    下载upx  onefile时压缩文件,  --plugin-enable=upx --upx-binary={upx}
    sudo apt update
    sudo apt install patchelf -y
    python -m nuitka --standalone --output-dir=out --show-progress --plugin-enable=upx --upx-binary=/root/pack_seckill/upx/upx pack_seckill.py
    ./pack_seckill.bin
```
### Ubuntu
```
    pip install ordered-set # 加速编译
    pip install nuitka
    pip install zstandard # onefile时压缩文件
    下载upx  onefile时压缩文件,  --plugin-enable=upx --upx-binary={upx}
    conda install libpython-static
    sudo apt-get update
    # gcc报错
    conda install gcc_linux-64
    conda install gxx_linux-64
    # 打包命令
    python -m nuitka --standalone --output-dir=out --show-progress --onefile --plugin-enable=upx --upx-binary=/home/ubuntu/pack_seckill/upx/upx pack_seckill.py
    sudo chmod +x ./pack_seckill.bin
    ./pack_seckill.bin
```
### 打包常用命令。使用nuitka --help可查看所有命令
```
    --mingw64 #默认为已经安装的vs2017去编译，否则就按指定的比如mingw(官方建议)
    --standalone 独立环境，这是必须的(否则拷给别人无法使用)
    --windows-disable-console 没有CMD控制窗口
    --output-dir=out 生成exe到out文件夹下面去
    --show-progress 显示编译的进度，很直观
    --show-memory 显示内存的占用
    --enable-plugin=pyside6
    --plugin-enable=tk-inter 打包tkinter模块的刚需
    --plugin-enable=numpy 打包numpy,pandas,matplotlib模块的刚需
    --plugin-enable=torch 打包pytorch的刚需
    --plugin-enable=tensorflow 打包tensorflow的刚需
    --windows-icon-from-ico=你的.ico 软件的图标
    --windows-company-name=Windows下软件公司信息
    --windows-product-name=Windows下软件名称
    --windows-file-version=Windows下软件的信息
    --windows-product-version=Windows下软件的产品信息
    --windows-file-description=Windows下软件的作用描述
    --windows-uac-admin=Windows下用户可以使用管理员权限来安装
    --linux-onefile-icon=Linux下的图标位置
    --onefile 像pyinstaller一样打包成单个exe文件(2021年我会再出教程来解释)
    --include-package=复制比如numpy,PyQt5 这些带文件夹的叫包或者轮子
    --include-module=复制比如when.py 这些以.py结尾的叫模块
```
