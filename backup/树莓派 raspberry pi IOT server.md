### 确保一切是最新版本

`sudo apt update
sudo apt upgrade`

### 下载IOTstack并重启
`
curl -fsSL https://raw.githubusercontent.com/SensorsIot/IOTstack/master/install.sh | bash
sudo shutdown -r now
`

### 进入文件夹，执行脚本
`
cd IOTstack/
./menu.sh
`
### 安装步骤
## 1.  脚本执行后进入build stack
![Image](https://github.com/user-attachments/assets/9063902c-28d2-4785-bccd-eb8926af70c1)

## 2. 选上需要的组件
- Grafana
- InfluxDB
- Mosquitto
- Node-RED 选上后提示issue，右键进入设置，安装默认一路回车键就行
- Portainer-CE 
![Image](https://github.com/user-attachments/assets/0e210c44-6c56-4c46-a1df-a79156ab8f95)

## 3. 去docker command 中 执行 Start stack 就会开始执行和安装配置好的组件
## 4. 查询当前container 
  `docker-compose ps`
## 5. 进入influxdb container 创建数据库

- 进入container启动数据库`docker exec -it influxdb influx`
- 创建数据库 `CREATE DATABASE hmi_data`
- 退出 `quit`

### 访问portainer
- 需要在启动后5分钟内在ip:9000进入界面设置用户名和密码

![Image](https://github.com/user-attachments/assets/73b54985-25bc-4652-bd66-2d87e065d5f3)

### 访问nodered
- ip:1880 (默认)
- 例子：

![Image](https://github.com/user-attachments/assets/963c5538-be85-4630-a909-fec87a3406c4)
- 点击mqtt
- 侧边弹窗点击 + （新建服务端 ）

![Image](https://github.com/user-attachments/assets/09ee742a-c6bf-4798-9c7c-292131d0529d)
- 配置 mqtt

![Image](https://github.com/user-attachments/assets/a87bdeb5-3f7f-43f1-8476-71e61dd04adf)

![Image](https://github.com/user-attachments/assets/c250f3bb-e191-42ff-9bc6-be9c14b8db04)

- 配置change node

![Image](https://github.com/user-attachments/assets/7f27002a-cdb4-4ec2-9b09-963dd66eb716)
输入
![Image](https://github.com/user-attachments/assets/16809bee-96a8-4a67-ab1d-8fcb7f85ad04)

-配置database

![Image](https://github.com/user-attachments/assets/c697aaa2-4ecd-4bb8-95c5-38dff850d872)

![Image](https://github.com/user-attachments/assets/1c32909b-8167-494d-86f9-34064b57b17d)

-部署

![Image](https://github.com/user-attachments/assets/32c17bc9-c73f-42e7-ba84-d9cd1095b0f2)

### 访问grafana
- IP:3000 (default)
- 初始用户名:admin
- 密码：admin
- 登陆后修改新密码
- 

![Image](https://github.com/user-attachments/assets/0f1c6d12-b36f-4b5b-b1ff-de61aba84d09)
- 选择influxdb
- 配置influxdb
![Image](https://github.com/user-attachments/assets/4f6d30c4-7ed2-498e-9e05-a5cfec0a66ae)
![Image](https://github.com/user-attachments/assets/8978c5c6-725c-4e89-84fd-57d459981ab0)
- 点击Save and test， 配置无误会显示datasource is working
- 创建dashboard
![Image](https://github.com/user-attachments/assets/7aa1b249-6043-4395-a993-12b12c6b6dc1)
![Image](https://github.com/user-attachments/assets/2cc4c578-e5e0-4dbd-972d-0b912b547c36)
- 点击save dashboard 保存
![Image](https://github.com/user-attachments/assets/5ac75427-5967-4cea-9dce-adfa15279a86)

# 完成

**来源： https://learnembeddedsystems.co.uk/easy-raspberry-pi-iot-server**