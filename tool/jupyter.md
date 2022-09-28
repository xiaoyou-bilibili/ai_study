> 这里是推荐直接使用conda来进行安装

## 安装
```shell
conda install -c conda-forge jupyterlab
```

## 配置
下面对jupyter进行一些自定义的配置
```shell
# 生成配置文件，成功后会显示配置文件的路径
jupyter lab --generate-config
# 比如我的是下面这个
vim /root/.jupyter/jupyter_lab_config.py
# 配置工作路径
c.NotebookApp.notebook_dir = '/code'
# 允许远程访问
c.ServerApp.allow_remote_access = True
# 设置监听ip
c.ServerApp.ip = '0.0.0.0'
# 允许root用户访问
c.ServerApp.allow_root = True

# 设置密码
jupyter lab password
# 会有下面的提示
[JupyterPasswordApp] Wrote hashed password to /root/.jupyter/jupyter_server_config.json
# 我们直接查看这个文件把获取到的密码配置到配置文件中
c.ServerApp.password = 'argon2:$argon2id$v=19$m=10240,t=10,p=8$Hgc0ePIs2aQuEG+iQo5YHQ$OdYUX3ot6baYgwPWOoZ3fipdXy8Brsw+Rm7rSBTnd+Y'

# 启动命令
jupyter lab
```




