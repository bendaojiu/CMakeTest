ADD_EXECUTABLE(hello main.cpp)


# 指定最终的目标二进制的位置
SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
SET(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)
# 在哪里 ADD_EXECUTABLE 或 ADD——LIBRARY，
# 如果需要改变目标存放路径，就在哪里加入上述的定义

# INCLUDE_DIRECTORIES([AFTER|BEFORE] [SYSTEM] dir1 dir2 ...)
# 1,CMAKE_INCLUDE_DIRECTORIES_BEFORE,通过 SET 这个 cmake 变量为 on,可以
# 将添加的头文件搜索路径放在已有路径的前面。
# 2,通过 AFTER 或者 BEFORE 参数,也可以控制是追加还是置前。

# LINK_DIRECTORIES(directory1 directory2 ...)

# TARGET_LINK_LIBRARIES(target library1
#                       <debug | optimized> library2
#                       ...)

# 特殊的环境变量 CMAKE_INCLUDE_PATH 和 CMAKE_LIBRARY_PATH
# 务必注意,这两个是环境变量而不是 cmake 变量。
# 使用方法是要在 bash 中用 export 或者在 csh 中使用 set 命令设置或者
# CMAKE_INCLUDE_PATH=/home/include cmake ..等方式。
# 这两个变量主要是用来解决以前 autotools 工程中
# --extra-include-dir 等参数的支持的。
# 也就是,如果头文件没有存放在常规路径(/usr/include, /usr/local/include 等),
# 则可以通过这些变量就行弥补。
# 我们以本例中的 hello.h 为例,它存放在/usr/include/hello 目录,所以直接查找肯
# 定是找不到的。
# 前面我们直接使用了绝对路径 INCLUDE_DIRECTORIES(/usr/include/hello)告诉工
# 程这个头文件目录。
# 为了将程序更智能一点,我们可以使用 CMAKE_INCLUDE_PATH 来进行,使用 bash 的方法
# 如下:
# export CMAKE_INCLUDE_PATH=/usr/include/hello
# 然后在头文件中将 INCLUDE_DIRECTORIES(/usr/include/hello)替换为:
# FIND_PATH(myHeader hello.h)
# IF(myHeader)
# INCLUDE_DIRECTORIES(${myHeader})
# ENDIF(myHeader)
# 上述的一些指令我们在后面会介绍。
# 这里简单说明一下,FIND_PATH 用来在指定路径中搜索文件名,比如:
# FIND_PATH(myHeader NAMES hello.h PATHS /usr/include
# /usr/include/hello)
# 这里我们没有指定路径,但是,cmake 仍然可以帮我们找到 hello.h 存放的路径,就是因
# 为我们设置了环境变量 CMAKE_INCLUDE_PATH。
# 如果你不使用 FIND_PATH,CMAKE_INCLUDE_PATH 变量的设置是没有作用的,你不能指
# 望它会直接为编译器命令添加参数-I<CMAKE_INCLUDE_PATH>。
# 以此为例,CMAKE_LIBRARY_PATH 可以用在 FIND_LIBRARY 中。
# 同样,因为这些变量直接为 FIND_指令所使用,所以所有使用 FIND_指令的 cmake 模块都
# 会受益。
