cmake_minimum_required(VERSION 3.0)
if (${COMiC_OS_GUI})

    add_library(__COMiC__os-gui_include INTERFACE)
    target_link_libraries(__COMiC__os-gui_include INTERFACE COMiC::types COMiC::os)
    target_include_directories(__COMiC__os-gui_include INTERFACE include)

    install(
            TARGETS __COMiC__os-gui_include
            PUBLIC_HEADER DESTINATION ./include
    )

    add_library(COMiC::os-gui::_include ALIAS __COMiC__os-gui_include)

    if (TARGET COMiC::os-gui)
        message("using external os-gui api")
    else ()
        add_subdirectory(windows)
        if (NOT TARGET COMiC::os-gui)
            message(FATAL_ERROR "current os doesn't support GUI, unset 'COMiC_OS_GUI' var")
        endif ()
    endif ()
else ()
    add_library(__COMiC__os-gui INTERFACE)
    target_include_directories(__COMiC__os-gui INTERFACE no-include)

    install(
            TARGETS __COMiC__os-gui
            PUBLIC_HEADER DESTINATION ./include
    )

    add_library(COMiC::os-gui ALIAS __COMiC__os-gui)
endif ()