# 概述

Cookie 是由 Web 服务器保存在用户浏览器（客户端）上的小文本文件。无论何时用户链接到服务器，Web 站点都可以访问 Cookie 信息。

# 实现代码
```javascript
var cookie = {
    //设置
    set: function (key, val, time) {
        let date = new Date();
        date.setTime(date.getTime()+time*24*3600*1000);//格式化为cookie识别的时间
        document.cookie = key + "=" + val + ";expires=" + date.toGMTString();//设置cookie
    },
    //获取
    get: function (key) {
      let getCookie = document.cookie.replace(/[ ]/g,"");  //获取cookie，并且将获得的cookie格式化，去掉空格字符
      let arrCookie = getCookie.split(";")  //将获得的cookie以"分号"为标识 将cookie保存到arrCookie的数组中
      let tips;  //声明变量tips
      for(let i=0;i<arrCookie.length;i++){   //使用for循环查找cookie中的tips变量
        let arr=arrCookie[i].split("=");   //将单条cookie用"等号"为标识，将单条cookie保存为arr数组
        if(key==arr[0]){  //匹配变量名称，其中arr[0]是指的cookie名称，如果该条变量为tips则执行判断语句中的赋值操作
          tips=arr[1];   //将cookie的值赋给变量tips
          break;   //终止for循环遍历
        }
      }
      return tips;
    },
    //清除
    clear: function (key) {
        cookie.set(key, '', -1);
    }
};
```
