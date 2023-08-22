### 升级内容
```
Kruise Rollouts 是一个旁路组件集成，提供高级渐进式交付功能：
  1.Deployment、CloneSet、StatefulSet、Advanced StatefulSet的多批量更新策略。
  2.金丝雀更新部署策略。

Pod TCP 监控功能呢：
  1. 普罗米修斯 Pod TCP 监控图表展示
```
### 1.前端插件安装
#### 插件拷贝至gin-vue-admin/web/src/plugin/ 目录，安装软件依赖
```
    npm i monaco-editor-vue3@0.1.6 js-yaml@4.1.0  \
          vue-chartjs@4.1.1 \
          xterm@4.19.0 \
          xterm-addon-fit@0.5.0 \
          js-base64@^3.7.3 \
          moment
```
### 2.后端插件安装
#### 插件放入gin-vue-admin/server/plugin，后端插件引入
gin-vue-admin/server/initialize/plugin.go 添加
```
import  "github.com/flipped-aurora/gin-vue-admin/server/plugin/kubernetes"

PluginInit(PrivateGroup, kubernetes.CreateKubernetesPlug()) // 
kubernetes插件
```
### 3.后端插件Websocket路由配置
gin-vue-admin/server/initialize/router.go
```
导入路由: 
   kubernetes "github.com/flipped-aurora/gin-vue-admin/server/plugin/kubernetes/router"
初始化路由里面加入插件配置(func Routers() *gin.Engine 初始化路由方法)
kubernetesRouter := kubernetes.RouterGroupApp.WsApiRouter 
{
    systemRouter.InitBaseRouter(PublicGroup)   // 注册基础功能路由 不做鉴权
    systemRouter.InitInitRouter(PublicGroup)   // 自动初始化相关
    kubernetesRouter.InitWsRouter(PublicGroup) // WebSocket路由 （这个是新增的路由）
  }
```
### 4.后端依赖安装
```
 gin-vue-admin 目录执行:    go mod tidy        #安装插件所需依赖
```

### 5.插件协助
已购买该插件，安装出现问题，请联系Gin-Vue-Admin获取插件作者联系方式 (当前插件处于促销期，两个月后会涨价，先到先得，莫失良机)

### 6.插件说明
[Github地址]https://github.com/2696524545/plugin/blob/main/README.md

### 7.插件购买地址
[Gin-Vue-Admin插件市场]https://plugin.gin-vue-admin.com/#/layout/newPluginInfo?id=42 

### 8.常见问题解答
[KubeConfig及Token凭据如何创建?]https://github.com/2696524545/plugin/blob/main/KubeConfig-Or-Token-Create.md

[Prometheus Operator 快速部署?]https://github.com/2696524545/plugin/blob/main/Prometheus-Operator.md

[Prometheus 数据查询过多，返回数据较大，导致Gin-Vue-Admin 操作日志会写入失败?]
```
Prometheus 数据查询过多，返回数据较大，导致Gin-Vue-Admin 操作日志会写入失败，修改字段类型：
表名:
   sys_operation_records
 
  字段名：  resp  修改为 longtext 类型

```
[MonacoEditor YAML 编辑器 鼠标定位不准问题？]
由于字体兼容性问题， 编辑器光标位置错误，解决办法：
注释全局font-family，文件路径 src/style/main.scss
![81B5DA41-8AB0-4DAE-8BB0-D0DA17E043FE](https://user-images.githubusercontent.com/5716348/221067415-735b0f41-406a-4678-a94d-b55add5a7b2c.png)

[Kruise Rollouts 金丝雀发布最佳实践]https://github.com/openkruise/rollouts/blob/master/docs/tutorials/basic_usage.md
[Kruise Rollouts 多批次发布最佳实践]https://openkruise.io/rollouts/user-manuals/strategy-multi-batch-update
[Kruise Rollouts A/B 测试发布策略最佳实践]https://openkruise.io/rollouts/user-manuals/strategy-ab-testing

### 9.功能展示
### 新功能（Kruise Rollouts 多批次发布）

![多批次发布](https://github.com/2696524545/plugin/blob/main/Kruise-Rollouts.gif?raw=true)

![集群管理](https://github.com/2696524545/plugin/blob/main/clusters.png?raw=true)
#### 集群管理
![集群管理](https://github.com/2696524545/plugin/blob/main/clusters.png?raw=true)
![集群管理](https://github.com/2696524545/plugin/blob/main/clusters3.png?raw=true)
#### 节点管理
![节点管理](https://github.com/2696524545/plugin/blob/main/node.png?raw=true)
#### 节点监控
![节点监控](https://github.com/2696524545/plugin/blob/main/nodemonitor.png?raw=true)
#### 工作负载
![工作负载](https://github.com/2696524545/plugin/blob/main/workloads.png?raw=true)
![工作负载](https://github.com/2696524545/plugin/blob/main/workload-form.png?raw=true)
#### Deployment详情
![Deployment详情](https://github.com/2696524545/plugin/blob/main/DeploymentDetail.png?raw=true)
#### Deployment编辑
![Deployment编辑](https://github.com/2696524545/plugin/blob/main/resourceEdit.png?raw=true)
#### Pod监控
![Pod监控](https://github.com/2696524545/plugin/blob/main/podmonitor.png?raw=true)
#### Pod终端
![Pod终端](https://github.com/2696524545/plugin/blob/main/PodTerminal.png?raw=true)
#### Pod终端日志
![Pod终端日志](https://github.com/2696524545/plugin/blob/main/podlogs.png?raw=true)
#### Pod管理
![Pod管理](https://github.com/2696524545/plugin/blob/main/Pods.png?raw=true)
#### 命名空间管理
![命名空间管理](https://github.com/2696524545/plugin/blob/main/namespaces.png?raw=true)
#### 网络管理
![网络管理](https://github.com/2696524545/plugin/blob/main/networks.png?raw=true)
![网络管理](https://github.com/2696524545/plugin/blob/main/network-form.png?raw=true)
#### 配置管理
![配置管理](https://github.com/2696524545/plugin/blob/main/configs.png?raw=true)
![存储管理](https://github.com/2696524545/plugin/blob/main/storages.png?raw=true)
#### 访问控制
![访问控制](https://github.com/2696524545/plugin/blob/main/access.png?raw=true)


## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=2696524545/plugin&type=Date)](https://star-history.com/#2696524545/plugin&Date)
