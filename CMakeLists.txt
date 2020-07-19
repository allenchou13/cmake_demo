cmake_minimum_required(VERSION 3.14)

set(CMAKE_INSTALL_PREFIX ${CMAKE_BINARY_DIR}/install CACHE PATH "")

project(trial)

add_library(${PROJECT_NAME}-static STATIC trial_lib.cpp trial_lib.h)
set_target_properties(${PROJECT_NAME}-static PROPERTIES
    OUTPUT_NAME ${PROJECT_NAME}_static
)

add_library(${PROJECT_NAME}-shared SHARED trial_lib.cpp trial_lib.h)
set_target_properties(${PROJECT_NAME}-shared PROPERTIES
    OUTPUT_NAME ${PROJECT_NAME}
)

include(GNUInstallDirs)
install(TARGETS ${PROJECT_NAME}-static ${PROJECT_NAME}-shared
    EXPORT ${PROJECT_NAME}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}$<$<CONFIG:Debug>:/debug>
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}$<$<CONFIG:Debug>:/debug>
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}$<$<CONFIG:Debug>:/debug>
)
install(FILES ${CMAKE_SOURCE_DIR}/trial_lib.h TYPE INCLUDE)
install(EXPORT ${PROJECT_NAME} DESTINATION lib/cmake/${PROJECT_NAME})


