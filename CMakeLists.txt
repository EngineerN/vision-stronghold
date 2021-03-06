CMAKE_MINIMUM_REQUIRED(VERSION 3.5)
project(Vision2016)

SET(EXEC_NAME ${PROJECT_NAME})

# Set Cxx Standard for use.
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set Cuda Static Runtime to be off
SET(CUDA_USE_STATIC_CUDA_RUNTIME OFF)

if(COMMAND cmake_policy)
	cmake_policy(SET CMP0003 OLD)
	cmake_policy(SET CMP0015 OLD)  
endif(COMMAND cmake_policy)

SET(EXECUTABLE_OUTPUT_PATH "${CMAKE_CURRENT_SOURCE_DIR}/bin")

find_package(OpenCV 2.4 COMPONENTS core highgui imgproc features2d gpu REQUIRED)

include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include) 

SET(SRC_FOLDER src)
SET(INCLUDE_FOLDER include)
Set(SOURCE ${SRC_FOLDER}/main.cpp ${SRC_FOLDER}/GearGripPipeline.cpp ${SRC_FOLDER}/ShooterGripPipeline.cpp)
Set(HEADERS ${INCLUDE_FOLDER}/GearGripPipeline.h ${INCLUDE_FOLDER}/GearGripPipeline.h ${INCLUDE_FOLDER}/WQueue.h ${INCLUDE_FOLDER}/CameraThread.h ${INCLUDE_FOLDER}/GearPipelineThread.h ${INCLUDE_FOLDER}/ShooterPipelineThread.h ${INCLUDE_FOLDER}/Config.h ${INCLUDE_FOLDER}/json.hpp)

# Check and add warning flags
set(GNU_WARNING_FLAGS -Wall -Wextra -pedantic)
add_compile_options("$<$<CXX_COMPILER_ID:GNU>:${GNU_WARNING_FLAGS}>")

add_executable(${EXEC_NAME} ${SOURCE} ${HEADERS})

TARGET_LINK_LIBRARIES(${EXEC_NAME} ${OpenCV_LIBRARIES})

