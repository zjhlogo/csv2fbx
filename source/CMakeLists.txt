cmake_minimum_required(VERSION 3.8)

project(ConvertCSV2FBX)

set(SOURCE_FILES
    checked.h
    CommonMath.cpp
    CommonMath.h
    ConvertCSV2FBX.cpp
    core.h
    CSVFile.cpp
    CSVFile.h
    FileStream.cpp
    FileStream.h
    unchecked.h
    )
group_sources("${SOURCE_FILES}")

add_executable(${PROJECT_NAME} ${SOURCE_FILES})
target_link_libraries(${PROJECT_NAME} ${PROJECT_ROOT}/external/fbxsdk/lib/libfbxsdk.lib)
target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_ROOT}/external/fbxsdk/include)

configure_runtime(${PROJECT_NAME} ${PROJECT_ROOT}/bin "")
