# link shared lib with full rpath
set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

add_executable(ibis ibis.cpp)
target_include_directories(ibis PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../src>)
target_link_libraries(ibis fastbit)

add_executable(tcapi tcapi.c)
target_include_directories(tcapi PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../src>)
target_link_libraries(tcapi fastbit)

add_executable(tiapi tiapi.c)
target_include_directories(tiapi PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../src>)
target_link_libraries(tiapi fastbit)

# "make install" rules
install(TARGETS ibis tcapi tiapi
        RUNTIME DESTINATION bin)
