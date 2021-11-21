cmake_minimum_required(VERSION 3.0)

add_library(__COMiC__os-gui_include INTERFACE)
add_library(COMiC::os-gui::_include ALIAS __COMiC__os-gui_include)

target_link_libraries(__COMiC__os-gui_include INTERFACE COMiC::types COMiC::os)

install(
        TARGETS __COMiC__os-gui_include
        PUBLIC_HEADER DESTINATION ./include
)

target_include_directories(__COMiC__os-gui_include INTERFACE include)

if (TARGET COMiC::os-gui)
    message("using external os api")
else ()
    add_subdirectory(windows)
    if (NOT TARGET COMiC::os-gui)
        message(FATAL_ERROR "current os not supported")
    endif ()
endif ()