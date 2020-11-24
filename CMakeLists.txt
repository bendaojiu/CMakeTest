cmake_minimum_required(VERSION 3.5)

PROJECT(HELLO)
ADD_SUBDIRECTORY(src bin)
ADD_SUBDIRECTORY(src/dy lib)
# ADD_SUBDIRECTORY(source_dir [binary_dir] [EXCLUDE_FROM_ALL])
# EXCLUDE_FROM_ALL 将这个目录从编译过程中排除

# 如果不指定 CMAKE_INSTALL_PREFIX 会默认安装到 /usr/local
# 安装 COPYRIGHT/README
INSTALL(FILES COPYRIGHT README DESTINATION doc)

# 安装 runhello.sh
INSTALL(PROGRAMS runhello.sh DESTINATION bin)

# 安装 hello.txt
INSTALL(DIRECTORY doc/ DESTINATION doc)

IF(WIN32)
# do something related to WIN32
ELSEIF(UNIX)
# do something related to UNIX
ELSEIF(APPLE)
# do something related to APPLE
ENDIF(WIN32)

# 添加模块查找路径
SET(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
