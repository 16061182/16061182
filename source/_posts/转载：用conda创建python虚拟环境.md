---
title: 转载：用conda创建python虚拟环境 
categories:  
- 转载 
tags:
- conda
- python
---
文章转载自[https://blog.csdn.net/lyy14011305/article/details/59500819](https://blog.csdn.net/lyy14011305/article/details/59500819)如有侵权请作者和我联系：983414728@qq.com

<p><span style="font-size:14px;">1、首先在所在系统中安装Anaconda。可以打开命令行输入conda -V检验是否安装以及当前conda的版本。<br></span></p>
<p><span style="font-size:14px;">2、conda常用的命令。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp; 1）conda list 查看安装了哪些包。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp; 2）conda env list 或 conda info -e 查看当前存在哪些虚拟环境</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp; 3）conda update conda 检查更新当前conda</span></p>
<p><span style="font-size:14px;">3、创建python虚拟环境。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp; &nbsp;使用 <span style="color:#ff0000;">conda create -n your_env_name python=X.X（2.7、3.6等)</span>命令创建python版本为X.X、名字为your_env_name的虚拟环境。your_env_name文件可以在Anaconda安装目录envs文件下找到。</span></p>
<p><span style="font-size:14px;">4、使用激活(或切换不同python版本)的虚拟环境。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp; 打开命令行输入python --version可以检查当前python的版本。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp; 使用如下命令即可&nbsp;激活你的虚拟环境(即将python的版本改变)。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp; Linux:&nbsp;<span style="font-size:14px;">&nbsp;</span><span style="font-size:14px;color:rgb(255,0,0);">source activate your_env_name</span><span style="font-size:14px;">(虚拟环境名称)</span></span></p>
<p><span style="font-size:14px;"><span style="font-size:14px;">&nbsp; &nbsp; Windows:&nbsp;<span style="font-size:14px;color:rgb(255,0,0);">activate your_env_name</span><span style="font-size:14px;">(虚拟环境名称)</span></span></span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp;这是再使用python --version可以检查当前python版本是否为想要的。</span></p>
<p><span style="font-size:14px;">5、对虚拟环境中安装额外的包。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp; 使用命令<span style="color:#ff0000;">conda install -n your_env_name [package]</span>即可安装package到your_env_name中</span></p>
<p><span style="font-size:14px;">6、关闭虚拟环境(即从当前环境退出返回使用PATH环境中的默认python版本)。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp;使用如下命令即可。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp;Linux:&nbsp;<span style="font-size:14px;"><span style="color:#ff0000;">source deactivate</span></span></span></p>
<p><span style="font-size:14px;"><span style="font-size:14px;"><span style="color:#ff0000;">&nbsp; &nbsp;</span>Windows:&nbsp;<span style="color:rgb(255,0,0);font-size:14px;">deactivate</span></span></span></p>
<p><span style="font-size:14px;">7、删除虚拟环境。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp;使用命令<span style="color:#ff0000;">conda remove -n your_env_name(虚拟环境名称) --all</span>， 即可删除。</span></p>
<p><span style="font-size:14px;">8、删除环境中的某个包。</span></p>
<p><span style="font-size:14px;">&nbsp; &nbsp;使用命令conda remove --name your_env_name&nbsp; package_name 即可。</span></p>

