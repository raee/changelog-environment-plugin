# Jenkins 日记记录写入环境变量插件

changelog-environment-plugin

Changelog Environment Plugin for JENKINS-12032


## 安装方法

先安装maven环境，没有的话可以[点击下载](http://maven.apache.org/download.cgi)

clone 下来后执行`mvn verify`， 过程比较久，稍等一下就好。

## 使用方法

安装成功以后，在项目配置的 `Build Environment` 环节，会多出一个选项：`Add Changelog Information to Environment`。

下面有三个编辑框，分别是：`Entry Format、File Item Format` 和 `Date Format`。

第一个就是填写提交日志输出格式的地方，采用的是 `Java String.format` 占位符的形式。其中可以使用四个参数，分别是：

- 提交的作者
- 提交的 ID
- 提交信息
- 提交时间(通过 Date Format 控制格式)

例如，我在 `Entry Format` 输入` %3$s (at %4$s via %1$s)\n`，然后有一条在 2017-02-10 的提交记录，提交信息为「fix bug」，提交者为 twiceYuan，那么输出到环境变量的字符串就是 “fix bug (at 2017-02-10 via twiceYuan)\n” (后面的 \n 是为了多层转义，视使用情况请自行调整)，同样时间格式编辑框填写的是：yyyy-MM-dd。

通过设置之后，在构建时就可以通过 shell 中来获得 `SCM_CHANGELOG` 变量来取到更新日志了。比如自动上传更新信息到内测平台。
