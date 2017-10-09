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

## 同步github：
### 生成public key
同步github需要配置sshkey先使用ssh-keygen命令生成key,提示需要输入密码时
可以按回车跳过，这里输入密码表示每次push时都需要输入密码，按下回车后以后每次`git push`时就不用输入密码了。
```
ssh-keygen -t rea -C "youremail@example"
```
s.g.

```
ssh-keygen -t rea -C "test@126.com"
```
![image_1b304rntm1jbk116m1k3p57m1hbs9.png-44.9kB][1]

执行成功后会在`C:\Users\账户名\.ssh`（linux会在`/home/用户名/.ssh`）目录下生成两个文件，不指定文件名和密钥类型的时候，默认生成的两个文件是：
```
id_rsa
id_rsa.pub
```
第一个是私钥文件（private key），第二个是公钥文件(public key)。
我们需要将公钥文件里面的内容添加到github上。
### 添加到github
在github setting里面的SSH and GPG keys里面点击new SSH keys:

![image_1bs0882tc1oj45gi19g41ehn10dr9.png-92.6kB][2]

名字随便填，key里面把刚刚生成的公钥文件里面的内容粘贴进来。

![image_1bs088v92kfvc7ftq14b41se6m.png-21.1kB][3]

一定要粘贴public key,一定要粘贴public key,一定要粘贴public key,然后提交表单就行了，
### 测试ssh keys是否设置成功
使用ssh -T 命令测试设置是否成功,如果出现
>You've successfully authenticated, but GitHub does not provide shell access.

表示设置成功
```
ssh -T git@github.com
```
![image_1b3053n67d731l18rha33arurm.png-10.8kB][4]


  [1]: http://static.zybuluo.com/danerlt/ahbmypha8g7xlmfzjpxkciv5/image_1b304rntm1jbk116m1k3p57m1hbs9.png
  [2]: http://static.zybuluo.com/danerlt/9i1a447bbu7622i2iqhreu01/image_1bs0882tc1oj45gi19g41ehn10dr9.png
  [3]: http://static.zybuluo.com/danerlt/ua0wv6swtqmrvne2fm0yatnx/image_1bs088v92kfvc7ftq14b41se6m.png
  [4]: http://static.zybuluo.com/danerlt/v1sema0z1dwyuiqykou6ucni/image_1b3053n67d731l18rha33arurm.png
