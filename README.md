# CVE-2017-10271

> Weblogic wls-wsat组件反序列化漏洞(CVE-2017-10271)检测脚本

### 用法

```bash
$ python CVE-2017-10271 url
```

另外需要注册一个`ceye.io`的账号，将其提供的`Identifier`及`API Token`填入代码的如下部分：

![mmp](mmp.png)

### 功能

检测Windows及Linux环境下Weblogic是否存在CVE-2017-10271的远程命令执行漏洞

<del>目前仅在Linux环境下测试过</del>

**Windows及Linux环境下均测试有效**

### 检测原理

使用`ceye.io`提供的DNS log功能以及其接口查询功能，通过发送ping命令，让服务器ping`ceye.io`提供的域名，并使用其查询接口查询是否收到这次ping的记录，来判断命令是否执行成功。

这里ping的域名采用随机6位大小写字母组成的字符串+ceye.io提供的域名组合而成，如`4xF7hY.xxxxxx.ceye.io`的形式，其中的`4xF7hY`在每次请求时随机生成，这样既方便在之后接口查询时可作为唯一特征值方便查询，也能确保漏洞检测的唯一性与准确性。

### 其他

此代码根据[@Lucifer1993](https://github.com/Lucifer1993)的[weblogic_xmldecoder_exec.py](https://github.com/Lucifer1993/AngelSword/blob/4ddf58550265ab26f4ca783872255a6d94635364/system/weblogic/weblogic_xmldecoder_exec.py)脚本整体架构基础上修改的，其中的`windows_payload`来自[@1337g](https://github.com/1337g)的[CVE-2017-10271](https://github.com/1337g/CVE-2017-10271)

