cmake_minimum_required(VERSION 2.8)

include_directories(${PROJECT_SOURCE_DIR}/include)
file(GLOB SOURCE_FILES "src/*.cpp")

set(BASE_LIBRARIES ${PROJECT_NAME} xstream gtest hobotlog jsoncpp pthread dl rt)
set(target_name ${PROJECT_NAME}_test)
add_executable(${target_name} ${SOURCE_FILES})
target_link_libraries(${target_name} VehiclePlateMatchMethod ${BASE_LIBRARIES})
