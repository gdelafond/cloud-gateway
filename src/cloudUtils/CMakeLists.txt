
find_package(LibXml2 REQUIRED)
if (LIBXML2_FOUND)
    include_directories(${LIBXML2_INCLUDE_DIR})
endif(LIBXML2_FOUND)

include_directories(include/)

find_package(NL REQUIRED)
include_directories(${NL_INCLUDE_DIRS})

file (GLOB_RECURSE
     source_files
     *.c
     )

add_library(cloudutils SHARED
                       cloudutils.c
                       cloudutils_file.c
                       cloudutils_htable.c
                       cloudutils_llist.c
                       cloudutils_network.c
                       cloudutils_pool.c
                       cloudutils_process.c
                       cloudutils_rbtree.c
                       cloudutils_regex.c
                       cloudutils_time_counter.c
                       cloudutils_vector.c)

add_library(cloudutils_advanced_file_ops SHARED cloudutils_advanced_file_ops.c)
add_library(cloudutils_aio SHARED cloudutils_aio.c)
add_library(cloudutils_configuration SHARED cloudutils_configuration.c)
add_library(cloudutils_crypto SHARED cloudutils_crypto.c)
add_library(cloudutils_encoding SHARED cloudutils_encoding.c)
add_library(cloudutils_event SHARED cloudutils_event.c)
add_library(cloudutils_http SHARED cloudutils_http.c)
add_library(cloudutils_json SHARED cloudutils_json_reader.c cloudutils_json_writer.c)
add_library(cloudutils_shm SHARED cloudutils_shared_memory_segment.c)
add_library(cloudutils_system SHARED cloudutils_system.c)
add_library(cloudutils_xml SHARED cloudutils_xml.c cloudutils_xml_reader.c cloudutils_xml_writer.c)

target_link_libraries(cloudutils m)
target_link_libraries(cloudutils_advanced_file_ops cloudutils cloudutils_aio)
target_link_libraries(cloudutils_aio cloudutils cloudutils_event evaio)
target_link_libraries(cloudutils_configuration cloudutils cloudutils_xml)
target_link_libraries(cloudutils_crypto cloudutils crypto)
target_link_libraries(cloudutils_encoding cloudutils crypto)
target_link_libraries(cloudutils_event cloudutils event)
target_link_libraries(cloudutils_http cloudutils cloudutils_event curl)
target_link_libraries(cloudutils_json cloudutils json-c)
target_link_libraries(cloudutils_shm cloudutils pthread rt)
target_link_libraries(cloudutils_system cloudutils ${NL_LIBRARIES})
target_link_libraries(cloudutils_xml cloudutils xml2)

set_target_properties(cloudutils PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_advanced_file_ops PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_aio PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_configuration PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_crypto PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_encoding PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_event PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_http PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_json PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_shm PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_system PROPERTIES VERSION 0.1 SOVERSION 1)
set_target_properties(cloudutils_xml PROPERTIES VERSION 0.1 SOVERSION 1)

install(TARGETS
                cloudutils
                cloudutils_advanced_file_ops
                cloudutils_aio
                cloudutils_configuration
                cloudutils_crypto
                cloudutils_encoding
                cloudutils_event
                cloudutils_http
                cloudutils_json
                cloudutils_shm
                cloudutils_system
                cloudutils_xml
                LIBRARY DESTINATION lib
                ARCHIVE DESTINATION lib
                PERMISSIONS OWNER_READ OWNER_WRITE GROUP_READ WORLD_READ)
