cmake_minimum_required(VERSION 2.8)
project(body_solution)

set(SOURCE_FILES
        main.cpp
        method_factory.cpp
        )

add_executable(${PROJECT_NAME} ${SOURCE_FILES})

set(BASE_LIBRARIES vioplugin smartplugin 
  visualplugin websocketplugin 
  bpu_predict ipc_tracking xstream 
  xstream-imagetools hobotlog vision_type_util 
  jsoncpp opencv_world 
       
  FasterRCNNMethod
  CNNMethod MOTMethod FilterMethod MergeMethod 
  vote_method BehaviorMethod LowPassFilterMethod
  DnnPredictMethod DnnPostProcessMethod
  MattingPredictMethod MattingPostProcessMethod
  MattingTrimapFreePredictMethod MattingTrimapFreePostProcessMethod
)

if (${PLATFORM_X2})
set(BASE_LIBRARIES CNNMethod ${BASE_LIBRARIES} )
endif()

if (${PLATFORM_X3})
set(BASE_LIBRARIES aioplugin ${BASE_LIBRARIES} uvcplugin )
endif()

target_link_libraries(${PROJECT_NAME} ${BASE_LIBRARIES})

set(MY_OUTPUT_ROOT ${OUTPUT_ROOT}/${PROJECT_NAME}/)
install(DIRECTORY
        ${CMAKE_CURRENT_SOURCE_DIR}/configs/
        DESTINATION ${MY_OUTPUT_ROOT}/configs/)
install(TARGETS ${PROJECT_NAME}
        DESTINATION ${MY_OUTPUT_ROOT}/)
