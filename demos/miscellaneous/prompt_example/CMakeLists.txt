project(PROMPT_EXAMPLE)

include_directories(${LIBMC_SOURCE_DIR}/src/include)
include_directories($ENV{CHHOME}/extern/include)
include_directories(../../../src/include)
#include_directories(/usr/local/ch7.0.0/extern/include)

add_executable(prompt_server1 server1.c)
add_executable(prompt_server2 server2.c)

#target_link_libraries(helloworld_server mc)
#target_link_libraries(helloworld_client mc)

if(CMAKE_HOST_WIN32)
target_link_libraries(prompt_server1 mc_static ws2_32 embedch chsdk)
target_link_libraries(prompt_server2 mc_static ws2_32 embedch chsdk)
else()
target_link_libraries(prompt_server1 mc_static embedch chsdk)
target_link_libraries(prompt_server2 mc_static embedch chsdk)
endif()
    
file(COPY "${CMAKE_CURRENT_SOURCE_DIR}/test1.xml" DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
file(COPY "${CMAKE_CURRENT_SOURCE_DIR}/helloworld.c" DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

