cmake_minimum_required(VERSION 3.12.0 FATAL_ERROR)


add_subdirectory(libtorrent)

#make internal functions visible in the .so
target_compile_definitions(torrent-rasterbar PUBLIC TORRENT_EXPORT_EXTRA)

add_subdirectory(fuzzers)
