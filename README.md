# log4z 轻量级跨平台c++日志库（android/linux/windows），支持日志信息简便过滤

经过测试log4z开源日志库在android平台上无法打印日志，所以修改使之能够同时兼容android平台，同时在原有基础上添加日志过滤功能

# 简单使用教程

#include "log4z.h"  
#include <iostream>  
#include <stdio.h>  
  
using namespace zsummer::log4z;  
          
int main(int argc, char *argv[])  
{  
    //启动LOG4Z  
    //没有添加任何日志记录器的情况下 LOG4Z会默认构建一个.  
    ILog4zManager::GetInstance()->Start();  
          
    //使用快速日志记录宏 可以快速把日志写入默认日志记录器中.  
    //LOGD对应 LOG DEBUG, LOGI对应LOG INFO 类推...  
    //该宏采用流的形式录入日志信息  
    LOGD(" *** " << "hellow wolrd" <<" *** ");  
    LOGI("loginfo");  
    LOGW("log warning");  
    LOGE("log err");  
    LOGA("log alarm");  
    LOGF("log fatal");  
   
    //停止LOG4Z   
    //如果不停止 将在程序退出时会安全销毁  
    //ILog4zManager::GetInstance()->Stop();  
    printf("press anykey to exit.");  
    getchar();  
    return 0;  
}  

# 日志过滤

    通过接口setLoggerFilter进行过滤掉不需要的日志信息或者选择需要的日志信息，这里修改了比较简单的字串处理规则，没有使用复杂的正则表达式进行匹配，
    主要是为了方便使用，如果需要更复杂的过滤功能，自行去修改源代码。
    
    LOG_T           ---- 选择包含LOG_T的日志信息
    ！LOG_T         ---- 过滤掉包含LOG_T的日志信息
    ！LOG_T|!LOG_A  ---- 过滤掉包含LOG_T或者包含LOG_A的日志信息
    
    ILog4zManager::getInstance()->setLoggerFilter(LOG4Z_MAIN_LOGGER_ID, "!LOG_T");
    //必须在启动前设置过滤规则
    ILog4zManager::getInstance()->start();






