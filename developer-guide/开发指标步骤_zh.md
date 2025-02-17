#  一、 使用grimoirelab拉取项目数据

```bash
cd /root/grimoirelab/default-grimoirelab-settings/
```

1. 新建需要抓取数据的项目json，项目分为gitHub项目和gitee项目两种，两种项目的项目json格式稍有不同，可以参考projects-gitee-template.json 和projects-github-template.json

2. 编辑 setup-gitee.cfg，其中[github:issue]等代表需要收集的数据

3. debug grimoirelab，需要在本地下载vscode，安装Remote Explorer插件，远程连接后在.vscode文件夹下新建 launch.json

   ``` json
   {
       "version": "0.2.0",
       "configurations": [
           {
               "name": "Python: Current File",
               "type": "python",
               "request": "launch",
               "program": "${file}",
               "console": "integratedTerminal",
               "justMyCode": false,
               "cwd": "${fileDirname}",
               "args": [
                   "--enrich",
                   "--raw", 
                   // enrich 和 raw 不可同时存在,需要先执行raw再 执行enrich
                   "--debug",
                   "--cfg",
                   "/home/lisongnan/grimoirelab/default-grimoirelab-settings/setup-gitee.cfg", //步骤2中的setup文件地址
                   "--backends",
                   "github:repo,github:issue",
                   "--logs-dir",
                   "logs"]
           }
       ]
   }
   ```

   ``` bash 
   执行函数 入口
   cd /root/repos/sirmordred/sirmordred/utils/
   micro.py
   ```
   
   

# 二、 指标开发

1.  进入已经安装的compass-metrics-model 目录下的/compass_metrics目录，可在原有的相关python文件下新增函数，即指标。 返回值需跟函数名保持一致
2. 将新开发的函数阈值配置在/compass_metrics/resources目录下的thresholds.yaml中
3. 需要将新开发的函数配置到compass_model 下的base_metrics_nodel.py中
4. 本地调试：在根目录下run_test.py中调用自己的指标

# 三、同步到Compass Lab

1. 在lab_metrics表中新增开发的指标

