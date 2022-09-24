# 租显卡进行训练

> 之前我训练模型一直都是本地在跑，我本地只有一块3060，显存只有12G，所以每次训练都要非常久，而且还要时刻小心爆显存。
>
> 而且因为cuda的限制，导致TensorFlow和pytorch的一些版本我本地跑不了，所以很多模型就被我直接放弃了
> 
> 基于以上两个原因，我选择了租显卡来训练，因为我跑模型只是学习，我也没那心思去不断调参，所以对我来说训练也不会用这么多时间，虽然租显卡比较贵，但是长期来看其实也还好

下面只介绍一些我用过的平台，以及这些平台常用功能的使用方法

## 恒源云平台
> 这个平台知乎上别人推荐的，目前先试用一段时间
### OSS常用命令
OSS一般用于存储数据集和打包训练好的模型，常用命令如下
```shell
# 登录OSS
oss login
# 创建文件夹
oss mkdir oss://datasets
# 把本地数据上传到云平台
oss cp 个人数据.zip oss://datasets/
# 查看所有数据
ss ls -s -d oss://datasets/
# 下载云平台的数据
oss cp oss://datasets/个人数据.zip /hy-tmp/
# 删除数据
oss rm oss://dataset_1
```

### 训练完模型后自动关机和上传训练结果
因为显卡是按秒计费的，所以我们训练完模型或者训练出现问题时最好及时关机和上传训练结果，可以省不少钱

首先可以在主函数里加上这样一段代码，最后面那个改成自己上传脚本所在路径
```python
try:
    main()
except Exception as e:
    print("err", e)
finally:
    os.system('/root/code/vits/upload.sh')
```

然后我们的上传脚本如下
```shell
#!/bin/bash
set -e

cd /hy-tmp
# 压缩包名称
file="result-$(date "+%Y%m%d-%H%M%S").zip"
# 把 result 目录做成 zip 压缩包
zip -q -r "${file}" result
# 通过 oss 上传到个人数据中的 backup 文件夹中
oss cp "${file}" oss://backup/
rm -f "${file}"

# 传输成功后关机
shutdown
```
最后给脚本加上执行权限
```shell
chmod u+x upload.sh
```



