cmake_minimum_required(VERSION 3.5)

SET(LIBHELLO_SRC hello.c)
ADD_LIBRARY(helloDLib SHARED ${LIBHELLO_SRC})
ADD_LIBRARY(helloSLib STATIC ${LIBHELLO_SRC})
# ADD_LIBRARY(libname
# [SHARED|STATIC|MODULE]
# [EXCLUDE_FROM_ALL]
# source1 source2 ... sourceN)
# 类型有三种:
# SHARED,动态库
# STATIC,静态库
# MODULE,在使用 dyld 的系统有效,如果不支持 dyld,则被当作 SHARED 对待。
# EXCLUDE_FROM_ALL 参数的意思是这个库不会被默认构建,除非有其他的组件依赖或者手
# 工构建。

# 指定输出位置
# SET(LIBRARY_OUTPUT_PATH ../../lib)
# 已在主 CMakeLists.txt 中指定

# 为了得到同名的动态库和静态库
# SET_TARGET_PROPERTIES(target1 target2 ...
# PROPERTIES prop1 value1
# prop2 value2 ...)
# 这条指令可以用来设置输出的名称,对于动态库,还可以用来指定动态库版本和 API 版本。
SET_TARGET_PROPERTIES(helloDLib PROPERTIES OUTPUT_NAME "hello")
SET_TARGET_PROPERTIES(helloSLib PROPERTIES OUTPUT_NAME "hello")

# 添加动态库版本号
SET_TARGET_PROPERTIES(hello PROPERTIES VERSION 1.2 SOVERSION 1)
# VERSION 指代动态库版本,SOVERSION 指代 API 版本。

# 安装
INSTALL(TARGETS helloDLib helloSLib
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)
# 静态库要用 ARCHIVE 关键字
INSTALL(FILES hello.h DESTINATION include/hello)
