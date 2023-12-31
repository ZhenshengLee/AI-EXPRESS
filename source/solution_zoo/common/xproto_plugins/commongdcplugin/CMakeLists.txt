cmake_minimum_required(VERSION 2.8)

# 项目名称
project(commongdcplugin)

# 添加头文件路径
include_directories(
    ${PROJECT_SOURCE_DIR}/include
)

# 头文件路径信息
file(GLOB PROJECT_INC
    "include/commongdcplugin/*.h"
)

# 源文件路径信息
file(GLOB PROJECT_SRC
    "src/commongdcplugin/*.cpp"
)

set(SOURCE_FILES ${PROJECT_SRC} ${PROJECT_INC})

add_library(${PROJECT_NAME} SHARED ${SOURCE_FILES})
set(BASE_LIBRARIES opencv_world pthread xproto xproto_msgtype
    hobotlog vision_type_util jsoncpp)
set(X3_HAPI_LIB vio hbmedia)
target_link_libraries(${PROJECT_NAME} ${BASE_LIBRARIES} ${X3_HAPI_LIB})


# make install才会安装
set(MY_OUTPUT_ROOT ${OUTPUT_ROOT}/${PROJECT_NAME})
install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/
    DESTINATION ${MY_OUTPUT_ROOT}/include/${PROJECT_NAME})
install(TARGETS ${PROJECT_NAME} DESTINATION ${MY_OUTPUT_ROOT}/lib)
install(DIRECTORY ${PROJECT_SOURCE_DIR}/configs/
    DESTINATION ${MY_OUTPUT_ROOT}/configs/)
