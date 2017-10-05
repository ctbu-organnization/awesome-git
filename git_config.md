# git配置
git有三种配置
- 系统配置  使用`git config --system 属性名 属性值`配置
- 用户配置  使用`git config --global 属性名 属性值`配置
- 仓库配置  使用`git config --local 属性名 属性值`配置

从下层往上层层覆盖，本教程只关心用户配置，也是最常用的。
安装完git的第一件事就是设置用户名和邮件地址:
```$xslt
git config --global user.name yourname
git config --global user.email  youremail
```
ps:yourname和youremail最好和github上保持一致 

同步github：

