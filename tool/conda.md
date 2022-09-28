> 以Ubuntu 22.04 来进行举例

## conda安装

下载地址：https://www.anaconda.com/products/distribution

下载后是一个sh文件，直接运行即可，安装过程就不赘述了

## 常用命令

```shell
# 环境列表
conda env list
# 创建一个新环境
conda create -n your_env_name python=x.x
# 环境激活
conda activate your_env_nam
# 退出环境
source deactivate
# 环境克隆
conda create -n new_env --clone old_env
# 环境删除
conda remove -n env_name --all
```