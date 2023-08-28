cmake_minimum_required( VERSION 3.24 )

set(PROJECT_NAME MultiConnectionClient)

project( ${PROJECT_NAME}
    VERSION 1.0.0
    LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package( Qt6 REQUIRED COMPONENTS
    Core
    Network
)

add_library( ${PROJECT_NAME} SHARED
    src/Client.cpp                  include/Client.h
)


set_target_properties( ${PROJECT_NAME} PROPERTIES VERSION ${PROJECT_VERSION} )
set_target_properties( ${PROJECT_NAME} PROPERTIES SOVERSION 1 )

# HEADERS --------------------------------------------------------------------------------

set_target_properties( ${PROJECT_NAME} PROPERTIES PUBLIC_HEADER include/Client.h)
target_include_directories( ${PROJECT_NAME} PRIVATE include)
target_include_directories( ${PROJECT_NAME} PRIVATE src)

# --------------------------------------------------------------------------------------------------


# INSTALLATION --------------------------------------------------------------------------------

include(GNUInstallDirs)
install(TARGETS ${PROJECT_NAME}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})


install(FILES ${CMAKE_BINARY_DIR}/MultiConnectionClient.pc
    DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)

# --------------------------------------------------------------------------------------------------

target_link_libraries( ${PROJECT_NAME}
    PRIVATE Qt6::Core
    PRIVATE Qt6::Network
)
