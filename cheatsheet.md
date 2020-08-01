## python3.7创建虚拟环境

>  用于创建和管理虚拟环境的模块称为 [`venv`](https://docs.python.org/zh-cn/3.7/library/venv.html#module-venv)。[`venv`](https://docs.python.org/zh-cn/3.7/library/venv.html#module-venv) 通常会安装你可用的最新版本的 Python。如果您的系统上有多个版本的Python，您可以通过运行 `python3` (python)或您想要的任何版本来选择特定的Python版本。
>
> 要创建虚拟环境，请确定要放置它的目录，并将 [`venv`](https://docs.python.org/zh-cn/3.7/library/venv.html#module-venv) 模块作为脚本运行目录路径: 

```
python -m venv tutorial-venv
```

如果它不存在，这将创建 `tutorial-env` 目录，并在其中创建包含Python解释器，标准库和各种支持文件的副本的目录。

创建虚拟环境后，您可以激活它。

在**Windows**上，运行:

```
tutorial-env\venv\Scripts\activate.bat
```

在这里，自己创建了FlaskProject目录下的虚拟环境，如下图所示。

![](https://gitee.com/haydnch/myImage/raw/master/imgs/enter.png)

![](https://gitee.com/haydnch/myImage/raw/master/imgs/venv.png)



## 推送一个本地标签

```
git push origin <tagname>
```

## 推送全部未推送标签

```
git push origin --tags
```

## 删除一个本地标签

```
git tag -d <tagname>
```
## 删除一个远程标签

```
git push origin :refs/tags/<tagname>
```

## 丢弃工作区修改

```
git checkout -- file
```

## 撤销暂存区修改

```
git reset HEAD <file>
```

## 从版本库删除文件

```
git rm file
git commit -m "remove"
```

## 版本回退

- 
  HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`


- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本

- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本

## 创建+切换分支

```
git checkout -b <name>或者git switch -c <name>
```

## 合并某分支到当前分支

```
git merge <name>
```

## 配置别名

```
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
git config --global alias.unstage 'reset HEAD'
```

## 启动redis

```
redis-server redis.windows.conf
```

### 启动服务

```
redis-server --service-start
```

### 关闭服务

```
redis-server --service-stop
```

## redis数据类型

> Redis支持五种数据类型：==string==（字符串），==hash==（哈希），==list==（列表），==set==（集合）及==zset==(sorted set：有序集合)。

## IDEA设置注释模版

默认methodReturnType()方法会返回全名。

例如：`@return java.util.List<java.util.Map<java.lang.String,java.lang.String>>`

如果@return 后面不想要返回类型的全名，可以在***return***参数的expression内填入：

> groovyScript("def result=''; def params=\"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split('<').toList(); for(i = 0; i < params.size(); i++) {if(i!=0){result+='<';};  def p1=params[i].split(',').toList();  for(i2 = 0; i2 < p1.size(); i2++) { def p2=p1[i2].split('\\\\.').toList();  result+=p2[p2.size()-1]; if(i2!=p1.size()-1){result+=','}  } ;  };  return result", methodReturnType())

就会变成`@return List<Map<String,String>>`

## 关于@Builder注解

有时为了在构造po类时，代码更优雅，会在po类加入@Builder注解，但因为@Builder和@Data一起使用时会将类的无参构造方法覆盖掉，会导致使用一些框架操作数据库时不能成功地将数据赋值给po类，例如myBatis。

在类中重写无参构造方法，防止与lombok的注解冲突，在无参构造方法上面加入**@Tolerate**注解。例如：

```java
@Data
@Builder
public class DataBuilder implements Serializable {

    @Tolerate
    public DataBuilder (){}
}
```

## vue无法加载

若要在本地计算机上运行您编写的未签名脚本和来自其他用户的签名脚本，请使用以下命令将计算机上的 执行策略更改为 RemoteSigned。

执行：`set-ExecutionPolicy RemoteSigned`

![](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200731085530171.png)

## npm设置淘宝镜像

```
npm config set registry https://registry.npm.taobao.org
```



