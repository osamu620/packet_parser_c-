cmake_minimum_required(VERSION 3.19)
project (PacketParser LANGUAGES CXX DESCRIPTION "JPEG 2000 codestream parser")

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if (CMAKE_CXX_COMPILER_ID MATCHES "Clang|GNU")
  set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-Wall -mtune=native -march=native")
endif()

if (CMAKE_CXX_COMPILER_ID MATCHES "Clang|GNU")
        set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS} -O0 -g -DDEBUG -fsanitize=address")
        set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS} -O2")
        set(CMAKE_CXX_FLAGS_RelWithDebInfo "${CMAKE_CXX_FLAGS} -O2 -g")
endif()

#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DSTACK_ALLOC")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

add_executable(jp2parser
        main.cpp
        utils.cpp
        j2k_header.cpp
        j2k_header.hpp
        j2k_packet.cpp
        j2k_packet.hpp
        j2k_tile.cpp
        j2k_tile.hpp
        tile_handler.hpp
)
set_target_properties(
        jp2parser
        PROPERTIES OUTPUT_NAME
        $<IF:$<CONFIG:Debug>,jp2parser,jp2parser_release>)