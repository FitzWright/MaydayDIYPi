#百分之百复制别人的项目，如需参考 请搜索 MaydayDIYPi  谢谢
# MaydayDIYPi
一个五月天相关的树莓派实验品    
目前进度：整体完成，正在细节调试中/画动画表情中     
未来可能尝试方向：使用触控屏幕增加更多操作模式/蓝牙联动场控    
## 材料准备    
树莓派 * 1[参考链接](https://ic-item.jd.com/100081906218.html)     
树莓派可接圆屏（触摸功能未来可能会用上）（可直接电商平台搜索单片机 圆屏，建议官方购买，比较便宜） * 1 [购买链接](https://www.waveshare.net/shop/1.28inch-LCD-Module.htm)     
USB音响 * 1(可以调成蓝牙模式)    
按钮 * 1（支持上下左右中键以及set和rst按钮）（建议让商家送线）[参考购买链接](https://item.jd.com/100016801309.html)    
P.S.:用树莓pi是因为存东西比较方便...如果想节省一点可以考虑便宜一点的单片机~
## 使用    
### 开启SPI与I2C接口（不然会报错找不到端口/文件）    
```
sudo raspi-config
Interfacing Options -> SPI -> Yes
Interfacing Options -> I2C -> Yes
```

### 安装屏幕运行库：
这里建议用Python3，因为其他代码里用到了2和3不一样的语法    
```
git clone https://github.com/WiringPi/WiringPi
cd WiringPi
./build
gpio -v
# 运行gpio -v会出现2.70版本，如果没有出现说明安装出错

#python2
sudo apt-get update
sudo apt-get install python-pip
sudo apt-get install python-pil
sudo apt-get install python-numpy
sudo pip install RPi.GPIO
sudo pip install smbus
sudo pip install spidev
#python3
sudo apt-get update
sudo apt-get install python3-pip
sudo apt-get install python3-pil
sudo apt-get install python3-numpy
sudo pip3 install RPi.GPIO
sudo pip3 install smbus
sudo pip3 install spidev

# 最新版树莓派如果安装包报错请参考以下命令
sudo apt install python3-RPi.GPIO
sudo apt install python3-smbus
sudo apt install python3-spidev
```


### 代码下载：    
```
git clone https://github.com/CaptainDra/MaydayFansDemo.git    
```   

### 运行(如果以后仓库改名请修改此处代码)：    
```
cd MaydayFansDemo/code
sudo python main.py
```
### 设置开机自启动：    
在 /home/pi/.config 下创建一个文件夹，名称为 autostart    
```
mkdir /home/pi/.config/autostart
```
在该文件夹下创建一个xxx.desktop文件，文件名以.desktop结尾，名称可自定义，文件的内容如下(请修改exec后变成main.py路径)：    
```
[Desktop Entry]
Name=example
Comment=My Python Program
Exec=python xxxx
Terminal=false
MultipleArgs=false
Type=Application
Categories=Application;Development;
StartupNotify=true
```
P.S.:这样自动启动进程需要通过杀进程方式来关闭

## 模块说明
### 显示模块
#### 小球运动说明
使用了五张相同表情来模拟动作，每张图片表情位移4个像素块（大约），运动速度为12加速-34减速，做往返运动，目前动作还比较单一

### 音乐模块
#### 音量控制说明
当音量大于0.1时，up为音量+0.1，
当音量小于0.1时，up为音量=0.1，
当音量大于0.1时，down为音量-0.1，
当音量小于0.1时，down为音量/2，

### 控制模块


## 台词显示功能
此功能为试验功能，只有连续输入↓↑↓↓↑↑↑↓↓↓↑↓然后按下rst才可以触发，会播放编号为99的歌曲并读取input.txt里边的文本    
预期是做成一个提词器/或者想写什么写什么就好了~

## 相关链接    
显示屏说明文档：[微雪L1.28](https://www.waveshare.net/wiki/1.28inch_Touch_LCD#.E8.BF.90.E8.A1.8C.E6.B5.8B.E8.AF.95.E7.A8.8B.E5.BA.8F)       


