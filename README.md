# OpenCV-Binocular-Vision-Face-Ranging

Hello！欢迎你来。

### 干嘛用的：

在你的电脑上连接两个摄像头，打开它们并把你的大脸放进对话框，我是说这样做的话你会获得你的脸到摄像头的距离。当然，你需要准备好两个摄像头和它们的矫正参数，没有这些参数的话就接着往下看吧。

### 环境需求：

我的配置：

Python-3.10.4

Opencv-4.5.5

如果需要运行Capture.ipynb的话：

imutils-0.5.4

MATLAB 2022a Update5

### 如何使用：

1.准备两个摄像头的矫正参数，已有请跳至第5步，若无请继续查看：

2.打印或者在你的平板上显示标定板图像，在电脑上连接摄像头，运行Capture.ipynb，按下“c”键对标定板进行拍摄。尽量在拍全的基础上多摆出一些不同的角度。进行至少15次拍摄，最好20次左右，拍摄完成后按下“q”键退出，现在你的左右相机图像应该被保存到了./left和./right下。

**注意：**

1. 我使用了两个摄像头，拥有两个USB接口，如果你是两个摄像头整合到一根USB线中，请修改Capture.ipynb中Cell2的部分，注意摄像头输出的尺寸，把画面正确的分开即可，[参考](https://blog.csdn.net/weixin_37857892/article/details/106319379)。
2. 修改Cell2中的Line4 和 5以适配你的摄像头分辨率和帧率。

3.打开MATLAB，在命令行输入：

```matlab
stereoCameraCalibrator
```

启动MATLAB的双目标定程序。

点击“Add Images”，在对话框中设定好步骤2中拍摄的照片的目录，注意左和右有区别。Pattern Seletion选择Checkerboard。测量你的标定板上一格的物理长度填写在Size of checkerboard square中，点击确定。

程序会弹出一个“Detection Results”对话框显示检测报告，Rejected stereo pairs值显示了你有多少对照片不合适未被添加并参与计算，注意要保证Added stereo pairs至少大于10，你可以选择查看，或者点击确定继续。

接下来你会看到程序对标定板定位的结果，需要检查每一对照片的原点（黄色方框）和XY轴是否位于同一方位，如果出现了不同方位的照片对，删除它。

点击右上角“Calibrate”，计算所需的数据！

底下的是表示图片奇异性的柱状图，如果你的图片数量够多建议多剔除一些不好的图片对，最后保留的图片对不少于10对。

计算完毕后点击“Export Camera Parameters”按钮。

4.回到MATLAB主界面，在工作区即可找到stereo Params，包含了相机内参以及左右相机的R、T矩阵。记录这些数据。

5.将数据写入binocular vision.ipynb的Cell2的USB_Camera类中，self.focal_length可以不用管。

**注意：**MATLAB界面的参数矩阵是按列排列的，也就是说每个分号隔开的是每一列而不是每一行，填写时需要注意！

6.现在万事俱备，按顺序执行binocular vision.ipynb文件即可。

## 参考：

链接：https://blog.csdn.net/weixin_37857892/article/details/106028162
