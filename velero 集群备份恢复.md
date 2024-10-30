velero 集群备份恢复


#### 1.minio 作为存储池
mkdir data 
vi  docker-compose.yml 
```
version: "3"
services:
  minio:
    image: minio/minio:latest
    container_name: minio
    ports:
      - "9000:9000"
      - "9001:9001"
    volumes: 
      - "./data:/data"
    environment:
      MINIO_ACCESS_KEY: "admin"
      MINIO_SECRET_KEY: "YRC5k3EyDZvq"
    command: server --console-address ':9001'  /data
    restart: always
    logging:
      driver: "json-file"
      options:
        max-size: "1m"
```

#启动容器
docker-compose up -d

访问web界面创建一个桶： velerodata


#### 2.安装 velero
```
 cat >velero-auth.txt << EOF
 [default]
 aws_access_key_id = admin
 aws_secret_access_key = YRC5k3EyDZvq
 EOF
```

下载适合的客户端版本 https://github.com/vmware-tanzu/velero/releases/
minio ip根据自己情况修改


velero install \
  --plugins velero/velero-plugin-for-aws\
  --provider aws \
  --bucket velerodata \
  --use-volume-snapshots=false \
  --secret-file ./velero-auth.txt \
  --backup-location-config region=minio,s3ForcePathStyle="true",s3Url=http://192.168.31.19:9000        

查看容器状态：
kubectl get pods -n velero



#### 3.velero常用操作

#不指定命名空间默认全部
velero backup create backup1         


#备份default命名空间下的资源
velero backup create data-backup --include-namespaces test  -n velero   --default-volumes-to-fs-backup

#删除备份
velero backup delete  data-backup

#下载备份
velero  backup download  data-backup 


#查看备份详情，最下测不能有错误信息，有错误信息，请查看velero pod日志
velero backup describe data-backup                                        

#查看备份日志
velero backup logs data-backup      


#查看备列表
velero backup   get  


#恢复
velero restore  create --from-backup data-backup  --wait  -n velero  