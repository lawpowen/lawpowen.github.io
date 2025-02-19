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

**来源： https://learnembeddedsystems.co.uk/easy-raspberry-pi-iot-server**