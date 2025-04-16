---
{"dg-publish":true,"permalink":"/仿真平台/box/【Mujoco】在Win10下的安装/","dgPassFrontmatter":true}
---

==百度网盘链接==：[MujocoWin10]( https://pan.baidu.com/s/1Pab_yRVsZuQs-TFiMXKbkg?pwd=e8dy )
提取码: e8dy 
## 1.mujoco仿真引擎安装

### 1.1 Visual Studio Build Tools的安装（两种方法可选，推荐第一种）
1. 直接安装Visual Studio 2017版本，勾选如图（==一定要勾选Windows 10 SDK(10.0.10240.0)，其他默认即可==），安装包见网盘链接中==Visual Studio2017(64bit).rar![](/img/user/仿真平台/attachment/Pasted image 20250415083701.png)==
2. 由于mujoco仿真引擎是基于C/C++的，因此我们==先要安装“Visual Studio Build Tools”==，这一步非常重要，不可跳过！再运行从百度网盘中下载的==“visualcppbuildtools_full.exe”==，勾选Windows 10 SDK，并点击安装。安装完成后，保险起见可以重启一下电脑再进行下一步。另外,“vs_buildtools.exe”是2017版本的Visual Studio Build Tools，用它安装也是可以的![](/img/user/仿真平台/attachment/Pasted image 20250415082834.png)
### 1.2 mjpro150_win64的安装

在 C:\Users\CangXi 路径下创建名为".mujoco"的文件夹。==注意，CangXi是我计算机的名称，大家需要改为自己的计算机名称==。将“mjpro150_win64.zip”中的文件解压至“.mujoco”中，形成如下图所示的安装目录![](/img/user/仿真平台/attachment/Pasted image 20250415084234.png)
**注意！mujoco文件夹内的子文件夹必须命名为“mjpro150”，不可用其他名字，否则后面会报错！**
当然，你也可以去官网下载“mjpro150_win64.zip”，下载链接：[Download](https://www.roboti.us/download.html)![](/img/user/仿真平台/attachment/Pasted image 20250415084427.png)
之后，将激活文件“mjkey.txt”（从2021.10开始，mujoco已经完全免费了，不用像以前一样申请试用啦！）放入“C:\Users\CangXi\.mujoco”和 “C:\Users\CangXi\.mujoco\mjpro150\bin”路径下。当然，你也可以去官网下载激活文件，下载链接：[License](https://www.roboti.us/license.html)![](/img/user/仿真平台/attachment/Pasted image 20250415084546.png)
### 1.3 配置环境变量

然后，再配置系统环境变量。先在“用户变量”和“系统变量”中，添加以下环境变量（==LENOVO-PC和CangXi改为自己的计算机名称==）

```text
变量名：MUJOCO_PY_MJPRO_PATH
变量值：C:\Users\LENOVO-PC\.mujoco\mjpro150

变量名：MUJOCO_PY_MJKEY_PATH
变量值：C:\Users\LENOVO-PC\.mujoco\mjpro150\bin\mjkey.txt
```
![](/img/user/仿真平台/attachment/Pasted image 20250415084617.png)
然后，再分别在“用户变量-Path”和“系统变量-PATH”中添加以下路径：

```text
C:\Users\CangXi\.mujoco\mjpro150\bin
C:\Users\CangXi\.mujoco\mjpro150
C:\Users\CangXi\.mujoco
```
![](/img/user/仿真平台/attachment/Pasted image 20250415084719.png)
配置完环境变量后，也可以重启一下电脑再进行下一步。因为windows 10上安装mujoco实在太多bug了，稍有不慎，就各自报错。
### 1.4 mujoco仿真引擎测试

至此，我们已经完成了第一步--mujoco仿真引擎的安装，可以通过在cmd控制台中输入以下命令来测试：

```text
cd C:\Users\CangXi\.mujoco\mjpro150\bin
simulate.exe ../model/humanoid.xml
```

如果一切顺利，你将看到![](/img/user/仿真平台/attachment/Pasted image 20250415084928.png)
## 2.安装mujoco-py

### 2.1创建虚拟环境

用Anaconda创建一个名为py37的虚拟环境（不能取名为mujoco，否则后面也会报错！）。如果还不知道Anaconda的同学建议先去了解Anaconda，简而言之它是一个环境管理器，这是搞Python必备的技能，在这里不过多讲解。在cmd控制台中，执行以下指令：

```text
conda create -n py37 python=3.7.0
```
![](/img/user/仿真平台/attachment/Pasted image 20250415085218.png)
### 2.2 解压并安装mujoco-py

千万不要直接pip install mujoco-py，否则各种bug会修得你怀疑人生。正确方法是去官网：[Releases · openai/mujoco-py](https://github.com/openai/mujoco-py/releases)下载“mujoco-py-1.50.1.0.tar.gz”或者“mujoco-py-1.50.1.0.zip”，二选一即可，并安装。![](/img/user/仿真平台/attachment/Pasted image 20250415085321.png)
这边我也已经将“mujoco-py-1.50.1.0.tar.gz”上传到百度网盘里了。将压缩包内的文件解压至“C:\Users\CangXi\.mujoco”路径下，打开cmd控制台，依次执行如下指令（# 后为注释，不要一起拷贝进控制台）：
```text
cd C:\Users\CangXi\.mujoco\mujoco-py-1.50.1.0  #进入解压后的目录
conda activate py37  #激活虚拟环境
pip install -r requirements.txt  #下载并安装相关依赖
pip install -r requirements.dev.txt  #下载并安装相关依赖
python setup.py install #安装mujoco-py
```
上面第三行和第四行命令如果下载得比较慢，可以用以下代码替换：
```text
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -r requirements.txt  #从清华源下载并安装相关依赖
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -r requirements.dev.txt  #从清华源下载并安装相关依赖
```
### 2.3 修改包位置
把下载的mujoco-py-1.50.1.0解压，把其中的mujoco_py文件夹复制，按个ctrl+C。![](/img/user/仿真平台/attachment/Pasted image 20250415090313.png)
粘贴到自己的python虚拟环境python包的所在位置，按个ctrl+V。![](/img/user/仿真平台/attachment/Pasted image 20250415090125.png)

例如，我python虚拟环境里下载的python包都在我的anaconda的torch环境里。
### 2.4 重装Cython
cython的需要重装为0.29.21版本，不然会报错  ![](/img/user/仿真平台/attachment/Pasted image 20250415090819.png)
```
pip install cython==0.29.21 -i https://pypi.tuna.tsinghua.edu.cn/simple
```
### 2.5 mujoco-py测试

至此，我们已经完成了第二步--mujoco-py的安装，可以用以下py脚本来测试：

```python
import mujoco_py
import os
mj_path, _ = mujoco_py.utils.discover_mujoco()
xml_path = os.path.join(mj_path, 'model', 'humanoid.xml')
model = mujoco_py.load_model_from_path(xml_path)
sim = mujoco_py.MjSim(model)
print(sim.data.qpos)
sim.step()
print(sim.data.qpos)
```

注意上述脚本需要在py37虚拟环境中运行。第一次执行可能会跳一大堆东西出来，不用担心，是在用1.1节安装的Visual Studio Build Tools构建一些东西。如果顺利，你将在最后看到：![](/img/user/仿真平台/attachment/Pasted image 20250415085654.png)
## 3.安装gym

#### 3.1 安装gym 
打开cmd控制台，依次执行以下命令：

```text
conda activate py37
pip install gym[mujoco]
```
#### 3.2 修改版本
```
pip install gym==0.20 -i https://pypi.tuna.tsinghua.edu.cn/simple
```
#### 3.3 测试
所有依赖都以安装完成，可以用以下py脚本进行测试（需要在py37虚拟环境中运行）：

```python
import gym
env = gym.make('HalfCheetah-v2')
env.reset()
done = False
while not done:
    _, _, done, _ = env.step(env.action_space.sample())
    env.render()
env.close()
```
![](/img/user/仿真平台/attachment/Pasted image 20250415091221.png)
## 4.强化学习算法测试

最后，推荐给大家一份比较轻便的强化学习算法代码实现，快去用PPO, TD3, SAC等算法与mujoco互动试试吧![](/img/user/仿真平台/attachment/Pasted image 20250415091309.png)[RL with Pytorch](https://github.com/XinJingHao/RL-Algorithms-by-Pytorch)
