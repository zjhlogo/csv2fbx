cmake_minimum_required(VERSION 3.8)

project(csv2fbx)

# Turn on the ability to create folders to organize projects (.vcproj)
# It creates "CMakePredefinedTargets" folder by default and adds CMake
# defined projects like INSTALL.vcproj and ZERO_CHECK.vcproj
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# Prevent creates default "CMakePredefinedTargets" folder
set_property(GLOBAL PROPERTY PREDEFINED_TARGETS_FOLDER "")

set(PROJECT_ROOT "${CMAKE_CURRENT_SOURCE_DIR}")
set(BIN_ROOT "${PROJECT_ROOT}/bin")

#---------------------------------------------------------------------------
# macros
#---------------------------------------------------------------------------
macro(group_sources SOURCE_FILES)
    foreach (FILE ${SOURCE_FILES})
        get_filename_component(PARENT_DIR "${FILE}" PATH)

        set(GROUP ${PARENT_DIR})
        # changes /'s to \\'s
        string(REPLACE "/" "\\" GROUP "${GROUP}")
        source_group("${GROUP}" FILES "${FILE}")
    endforeach ()
endmacro()

macro(configure_library PROJ_NAME FOLDER_NAME)
    set_target_properties(${PROJ_NAME} PROPERTIES OUTPUT_NAME_DEBUG ${PROJ_NAME}_D)
    set_target_properties(${PROJ_NAME} PROPERTIES OUTPUT_NAME_RELEASE ${PROJ_NAME})
    if (NOT ${FOLDER_NAME} STREQUAL "")
        set_target_properties(${PROJ_NAME} PROPERTIES FOLDER ${FOLDER_NAME})
    endif ()
endmacro()

macro(configure_runtime PROJ_NAME OUTPUT_PATH FOLDER_NAME)
    set_target_properties(${PROJ_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_PATH})
    set_target_properties(${PROJ_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_DEBUG ${OUTPUT_PATH})
    set_target_properties(${PROJ_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_RELEASE ${OUTPUT_PATH})
    set_target_properties(${PROJ_NAME} PROPERTIES OUTPUT_NAME_DEBUG ${PROJ_NAME}_D)
    set_target_properties(${PROJ_NAME} PROPERTIES OUTPUT_NAME_RELEASE ${PROJ_NAME})
    set_target_properties(${PROJ_NAME} PROPERTIES VS_DEBUGGER_WORKING_DIRECTORY ${OUTPUT_PATH})
    if (NOT ${FOLDER_NAME} STREQUAL "")
        set_target_properties(${PROJ_NAME} PROPERTIES FOLDER ${FOLDER_NAME})
    endif ()
endmacro()

#---------------------------------------------------------------------------
# sub modules
#---------------------------------------------------------------------------
add_subdirectory(source)
