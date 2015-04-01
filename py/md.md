<meta http-equiv="content-type" content="text/html; charset=UTF-8">
# Mirror Smart devices
---------
## 包含内容

* [BroadLink](http://www.broadlink.com.cn/home/) [Code](/Common/Mirror/MirrorPad/src/com/nokee/mirrorpad/broadlink) 
* [时云体脂分析仪](http://www.rysmart.com/index.html) [Code](Common/Mirror/MirrorPad/src/com/nokee/mirrorpad/device/shiyun) 

### 时云体脂分析仪
#### 文件清单：
	-DeviceUtils.java
	-domain
		-ShiYunTestInfo.java
		-ShiYunUser.java
    -db
		-DataBaseUtils.java
		-ShiYunDbUtils.java
	-shiyun
		-BleScreenReciver.java
		-BleScanService.java
		-BleShiYunInfoUI.java
		-BleShiYunManagerUI.java
		-BleShiYunTestAnalysisUI.java
		-BleShiYunTestUI.java
		-BleShiYunUserAddSuccessUI.java
		-BleShiYunUserAddUI.java
		-BleShiYunUsersUI.java
		-BleShiYunWelUI.java
		-ShiYunUserGvAdapter.java
#### 具体文件解释
domain:实体内容 包括 用户实体，和测试结果实体

DeviceUtils.java 存放一些 和智能设备有关的 工具

DataBaseUtils.java 实现时云数据库的创建

```
public class DataBaseUtils {
	private static class DbHolder {
		public static DbUtils DB_UTILS(Context context) {
			// TODO Auto-generated
			// method stub
			return DbUtils.create(context, Constants.DB_DEVICE_NAME);
		}
	}
	public static DbUtils getInstance(Context context) {
		// TODO Auto-generated method
		// stub
		return DbHolder.DB_UTILS(context);
	}

}

```
		





