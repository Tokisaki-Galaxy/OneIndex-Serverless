# OneIndex-Serverless
# [原始项目连接](https://github.com/LiuChangFreeman/OneIndex-Serverless)

## 说明
本项目是[OneIndex](https://github.com/donwa/oneindex)的阿里云[函数计算](https://help.aliyun.com/document_detail/51733.html)版本,您无需拥有一台服务器，即可拥有属于自己的OneDrive云盘
## 为什么本项目选择Serverless?

1. 成本极其低廉，穷人也能用得起。完全实现按使用量(访问量)付费，费率极低，并且无固定费用支出
2. 不需要自行管理服务器，运行极其稳定。而且服务的质量不受配置(带宽、内存、硬盘......)的影响
3. 极为方便地搭配其他云计算产品进行优化。比如使用CDN对静态页面加速，同时降低流量成本

## 基本部署流程
### 后端部分
* 注册您的阿里云账号，获取accessKey和accessKeySecret
* 开通**对象存储**与**函数计算**服务
* 创建一个存储桶和一个云函数，上传Flask程序，并填写必要的配置
### 前端部分
* 将函数计算的http触发器url填写到config.json中
* 使用任意一种部署静态资源的方法将index.html和config.json部署到网络上
* 在浏览器中访问index.html，并在后台登录您的OneDrive账号

详细教程请参考[部署教程](https://zhuanlan.zhihu.com/p/74538287)

---

# 部署包
```Front```和```Back```文件夹分别是已编译的前端网页和后端源代码

其中```Back/mian.py```中您需要修改这几行配置信息
```
password="123456"#后台管理的密码
url_host= "".strip("/")
#http触发器的接口url


access_key=''#云账号的AccessKey
access_key_secret=''#云账号AccessKey的密码
oss_end_point= 'http://oss-cn-shanghai-internal.aliyuncs.com'#访问对象存储的endpoint
oss_bucket_name='sample bucket name'#可以使用的对象存储桶名称
```
```Front/config.json```中需要将```host```字段修改为```main.py```中相同的http触发器的url

Front文件夹下仅含有两个部署文件，您可以使用任意一种方法将前端网页部署到网络上，如iis、nginx、httpd。甚至您可以直接用GitHub Pages等静态网页托管服务。
