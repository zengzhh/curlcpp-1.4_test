使用curlcpp.lib
=======

1.首先编译curlapp.lib

https://github.com/zengzhihua24/curlcpp/tree/1.4

2.引入curlcpp和curl的头文件、curlcpp.lib  
```
thirdparty
  include\
    curl\
      curl.h
      ...
    curlcpp\
      cookie.h
      ...
  Win32\
    lib\
      curlcpp.lib
```

3.配置工程
```
输出目录：$(ProjectDir)$(Configuration)\$(Platform)\
中间目录：$(OutDir)temp\
附加包含目录：$(SolutionDir)thirdparty\include
附加库目录：$(SolutionDir)thirdparty\$(Platform)\lib
附加依赖项：curlcpp.lib
```

4.编写运行代码
```cpp
#include "curlcpp\curl_easy.h"
using curl::curl_easy;
using curl::curl_easy_exception;
/**
* This example shows how to make a simple request with curl.
*/
int main() {
    // Easy object to handle the connection.
    curl_easy easy;
    // Add some options.
    easy.add<CURLOPT_URL>("www.baidu.com");
    easy.add<CURLOPT_FOLLOWLOCATION>(1L);
    try {
        // Execute the request.
        easy.perform();
    } catch (curl_easy_exception &error) {
        // If you want to get the entire error stack we can do:
        auto errors = error.what();
        // Otherwise we could print the stack like this:
        error.print_traceback();
    }
    return 0;
}
```
