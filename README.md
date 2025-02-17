# daily-study
show experience  which is got from daily study
# GUNS_process
整理一下如何上传前后端的流程

# 20250111 新增

[谷歌大模型 Gemini 官网](https://aistudio.google.com/app/prompts/new_chat)

![alt text](fig/image-17.png)

`Prompt`:

```
给你一个语义管理模块下的功能操作，包含「功能名称」 下的 「子功能操作」
请根据 「子功能操作」 中抽取出一个vision流程图
```

```
子模块：XXX
功能：XXX
功能操作：XXX
操作说明：XXX
```

将生成的代码复制到：[这个网页](https://mermaid.live/edit#pako:eNpVkEFrhEAMhf9KyKkF_QMeCl1t97Klhe6p6iFodIZ1JsM4sizqf--4ttDmlPC-9whvxkZaxgy7Qa6NIh_gXFQW4jyXufJ6DIbGGtL0aTlyACOWbwscHo4CoxLntO0fd_6wQZDPpw1jCErby7pL-d3_bnmBojyRC-Lqv8r5Kgu8lPpDxfj_ivIcXa9lR1lHaUMecvI1JmjYG9JtfH3eDBUGxYYrzOLackfTECqs7BpRmoJ83myDWfATJ-hl6hXGvGGM1-RaClxo6j2ZX4RbHcS_7d3cK0rQkf0SMT_G9RsZb2ap)

![alt text](fig/image-18.png)

# 20250107 新增

- 注意表格的框线，不要少
- 把 ID 删掉

# 20250105 新增

1. 保持`语法通顺`的前提下，**删除口语化表述的词语**：

- 「人称词」，们，自己，了
- 最后，此外，最终，这方面，然后，总而言之，重要的是，关键的是，接着，不过，这样，那样，这边，那边，这个，那个
- 很，非常，太，一点，好多，挺多
- 本文，实验证明

2. **Visio 图：**
- 所有的流程图都需要`开始`、`结束`节点
- 不要密密麻麻
- 方框内不要空白太多，方框间间距协调
- 字体用微软雅黑；字号在Word上比标题小，但清晰可见
- 框线粗细 1pt

## Requirement
1. Java JDK 1.8
2. NodeJS 18+
3. Maven 3.6+

## Dependency
1. 打开`guns-8.1.2-roses-kernel`文件夹，执行`mvn clean install`命令，将核心包安装到本地仓库
2. 打开`guns-8.1.2-enterprise-plugins`文件夹，执行`mvn clean install`命令，将企业版插件核心包安装到本地仓库

## 启动后端

需要更改的`settings`:
1. guns version 1.8
![alt text](fig/image.png)
2. 修改 maven 配置
![alt text](fig/image-1.png)
3. 设置 `model-platform-yx/guns-8.1.2-backend/src/main/java` 为 Source root, (右键 -> Mark Directory as -> Sources Root)
4. 设置 `model-platform-yx/guns-8.1.2-backend/src/main/resources` 为 Resource root, (右键 -> Mark Directory as -> Resource Root)
5. 打开guns-8.1.2-backend启动后端即可

## 启动前端

打开`model-platform-yx/guns-8.1.2-front`

执行`npm run dev`命令，即可启动项目

# 在 SQL 中生成表

连接服务器上的数据库

把建表语句输入`新建查询`中，点击运行

![alt text](fig/image-6.png)

推荐先在SQL中生成表，可以找到一些报错

# 如何建表

- 这一部分可以同时参考PDF《代码生成及菜单配置》

    https://gunsdevops.com/login 注册并登陆

## 在GUNS生成表

-> 0 [Button] `开始使用`

-> 1 [左侧边栏] `应用设计`

-> 2 `数据表`

![alt text](fig/image-4.png)

-> 3 [右侧上方] `导入SQL`

-> 4 粘贴自己的 SQL 代码
- 把 `float` 改成 `decimal(x,y)`

    x, y 需要根据需要自己设置, x 为一共有几位数，y 为小数点后有几位数

- 把 `boolean` 改成 `char(1)`
- 把 `enum('x', 'y', 'z')` 改成 `char(1)` (不超过10个的话)

-> 5 点击`确定`

-> 不断重复3,4,5 直到这个子模块的表全部导入

## 生成后端代码

-> 1 [左侧边栏] `应用生成`

-> 2 [上面边栏] `代码生成`

-> 3 `后端代码`

![alt text](fig/image-3.png)

开始建立后端代码，红框部分请根据自己的模块进行修改

![alt text](fig/image-2.png)

-> 4 将我的分类中所有输入这个子模块的表导入进去 (一般是最后几个)

-> 5 点击`生成代码`

-> 6 点击`打包下载`

## 生成前端代码

-> 1 [左侧边栏] `应用生成`

-> 2 [上面边栏] `代码生成`

-> 3 `前端代码`

开始建立前端代码，红框部分请根据自己的模块进行修改

![alt text](fig/image-5.png)

-> 4 将我的分类中所有输入这个子模块的表导入进去 (一般是最后几个)

-> 5 点击`生成代码`

-> 6 点击`打包下载`

# 如何把GUNS生成的代码部署到当前代码中


## 后端代码部署

1. 将下载的后端代码解压，将解压后的文件夹拷贝到`guns-8.1.2-backend/src/main/java/cn/stylefeng/guns/modular`相应的模块中
2. 修改所有 `controller` 中的导入包
   ![alt text](fig/image-7.png)
    a. 删除红色的行

    b. 在 @Resource 上 按快捷键 `Alt + Enter` （mac 上是 `Option + Enter`） 选择 `Add module dependency`，选择当前模块

    ```java
    import javax.annotation.Resource;
    ```

    c. 在所有的 `...Controller` 中 执行 a,b 步骤 (有几个表就有几个 `...Controller` )
3. 修改所有 `pojo.request` 中的导入包
   ![alt text](fig/image-8.png)
    a. 删除红色的俩行

    b. 在 `@NotNull` 上 按快捷键 `Alt + Enter` （mac 上是 `Option + Enter`） 选择 `javax` 的 `@NotNull`

    c. 在 `@NotBlank` 上 按快捷键 `Alt + Enter` （mac 上是 `Option + Enter`） 选择 `javax` 的 `@NotBlank`

    ```java
    import javax.validation.constraints.NotBlank;
    import javax.validation.constraints.NotNull;
    ```

    d. 在 所有的 `...Request` 中 执行 a,b,c 步骤 (有几个表就有几个 `...Request` )
4. 修改所有 `pojo.response` 中的导入包
    ![alt text](fig/image-9.png)
    a. 在第一行 上 按快捷键 `Alt + Enter` （mac 上是 `Option + Enter`） 选择 上图中红框的包

    b. 在 所有的 `...Vo` 中 执行 a 步骤 (有几个表就有几个 `...Vo` )

## 前端代码部署

1. 在 `guns-8.1.2-front/src/views/` 自己的模块下面 **建立 一个当前子模块的文件夹** （与生成后端代码的的项目包名对应），将下载的前端代码解压，将解压后的文件夹拷贝到这个文件夹中

# 建立菜单

- 这一部分可以同时参考PDF《代码生成及菜单配置》

## 建立一级目录

-> 1 点击`应用`

-> 2 点击`后台管理`

![alt text](fig/image-10.png)

-> 3 点击`应用`

-> 4 点击`新建`

![alt text](fig/image-11.png)

-> 5 根据自己子系统输入相应的信息

![alt text](fig/image-12.png)

## 建立二级目录

-> 1 点击`菜单`

-> 2 在最右边滑动到自己的子系统

![alt text](fig/image-13.png)

-> 3 按照图示步骤修改为自己的二级目录信息

`链接地址` 与 `路由地址` 一致

## 建立三级目录

-> 1 点击相应二级目录的`新建`

![alt text](fig/image-14.png)

-> 2 按照图示步骤修改为自己的三级目录信息

![alt text](fig/image-15.png)

`路由地址`为前端代码中的vue地址：

![alt text](fig/image-16.png)

`链接地址` 与 `路由地址` 一致

添加完第一个三级目录后，请重启前后端代码，确保菜单能够正常显示后，再继续添加余下三级目录
