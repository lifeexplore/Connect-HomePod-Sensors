目的：将HomePod的温度和湿度传感器数据实时传入HomeAssistant
说明：由于本人的HomeAssistant是安装在Docker上，如果是其它方式安装的，可能需要一些必要的修改

需要的平台：
	1. HomeAssistant
	2. Node-Red
	3. IOS可以需要16以上
	
原理：
	1. 由于IOS的不开放，不可能从其它的软件访问IOS内部的数据，也不可能直接放访问Homepod获得数据，因此只能定时由IOS将数据送给HoneAssistant。
	2. 分工：
		a. 传感器在HomeAssistant下定义；
		b. 由于Homekit不能定时触发事件，HomeAssistant提供Homekit Bridge定时触发Homekit的自动化进程；
		c. Homekit将传感器的数据送到HomeAsssitant的实体中。
		
主要的参考：
	https://community.home-assistant.io/t/how-to-integrate-homepod-mini-sensors-into-home-assistant-when-direct-integration-isnt-possible/665074/3	    
		    
步骤：
	1. 在configuration.yaml中增加定义boolean；
	2. 通过Homekit Bridge将boolean传递给Homekit；
	3. 定义传感器；
	4. 设置HomeAssitant下的自动化：timer_to_homekit；
	4. 设置Homekit的自动化进程。