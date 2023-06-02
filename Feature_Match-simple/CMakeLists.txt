# CMake 最低版本号要求2.8
cmake_minimum_required(VERSION 2.8)

# 项目名称feature_match
project(feature_match)

# 设置编译方式Release
set(CMAKE_BUILD_TYPE Release)

# 支持C++11 -o3优化
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -o3")

# 查找系统里的OpenCV，找不到输出警告信息
find_package(OpenCV REQUIRED)

# 添加项目包含路径
include_directories(${PROJECT_SOURCE_DIR}/include
                    ${OpenCV_INCLUDE_DIRS})

message(${PROJECT_SOURCE_DIR})
add_library(VFC_LIBS ${PROJECT_SOURCE_DIR}/source/vfc.cpp)


# 用源文件为工程添加可执行文件，名字和项目名称一致
add_executable(${PROJECT_NAME} ${PROJECT_SOURCE_DIR}/source/feature_matcher.cpp)

# 可执行文件添加库链接
target_link_libraries(${PROJECT_NAME}
                      ${OpenCV_LIBS}
                      VFC_LIBS)
