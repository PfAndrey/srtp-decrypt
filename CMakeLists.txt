cmake_minimum_required(VERSION 3.5)
project(Srtp-Decrypt VERSION 0.99 LANGUAGES C CXX)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17")
 
if(NOT CMAKE_BUILD_TYPE)
 set(CMAKE_BUILD_TYPE "Release")
endif()

set(SOURCE
	${CMAKE_SOURCE_DIR}/source/rtp.h
	${CMAKE_SOURCE_DIR}/source/rtp.c
	${CMAKE_SOURCE_DIR}/source/rtp_decoder.c
	${CMAKE_SOURCE_DIR}/source/rtp_decoder.h
	${CMAKE_SOURCE_DIR}/source/getopt_s.h
	${CMAKE_SOURCE_DIR}/source/getopt_s.c
	${CMAKE_SOURCE_DIR}/source/util.h
	${CMAKE_SOURCE_DIR}/source/util.c
	${CMAKE_SOURCE_DIR}/source/config.h
)
 
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/external/librstp/include)
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/external/wpcap/include)

link_directories(${CMAKE_SOURCE_DIR}/external/librstp/lib 
			${CMAKE_SOURCE_DIR}/external/wpcap/lib )

# ADD EXECUTABLE
add_executable(srtp-decrypt ${SOURCE})

target_link_libraries(srtp-decrypt Packet wpcap srtp2 Ws2_32)

if (MSVC)
	set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT srtp-decrypt)
endif(MSVC)
 