project(FIPA_JADE)

include_directories(${LIBMC_SOURCE_DIR}/src/include)
include_directories($ENV{CHHOME}/extern/include)
include_directories(../../../src/include)
#include_directories(/usr/local/ch7.0.0/extern/include)

add_executable(fipa_jade_server server.c)

#target_link_libraries(helloworld_server mc)
#target_link_libraries(helloworld_client mc)

if(CMAKE_HOST_WIN32)
target_link_libraries(fipa_jade_server mc_static ws2_32 embedch chsdk)
else()
target_link_libraries(fipa_jade_server mc_static embedch chsdk)
endif()


file(GLOB xmlFiles "${CMAKE_CURRENT_SOURCE_DIR}/*.xml")
foreach(xmlFile ${xmlFiles})
    file(COPY ${xmlFile} DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
endforeach()

file(COPY "${CMAKE_CURRENT_SOURCE_DIR}/fipa_message.txt" DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
file(COPY "${CMAKE_CURRENT_SOURCE_DIR}/http_message.txt" DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
