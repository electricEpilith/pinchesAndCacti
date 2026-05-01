cmake_minimum_required(VERSION 3.22...4.2)

project(pinchesAndCacti
    LANGUAGES C
)

include(FetchContent)

FetchContent_Declare(sonLib
    GIT_REPOSITORY https://github.com/electricEpilith/sonLib.git
    GIT_TAG        6ea5147f19f46e3140831b54af058dcd622f885f
    EXCLUDE_FROM_ALL
)
FetchContent_MakeAvailable(sonLib)

add_library(threeEdgeConnected STATIC
    externalTools/threeEdgeConnected/impl/3_Absorb3edge2x.c
)
target_include_directories(threeEdgeConnected PUBLIC externalTools/threeEdgeConnected/inc)
target_link_libraries(threeEdgeConnected PRIVATE sonLib)

add_library(pinchesAndCacti STATIC
    impl/stCactusGraphs.c
    impl/stPinchGraphs.c
)
target_include_directories(threeEdgeConnected PUBLIC inc)
target_link_libraries(pinchesAndCacti PRIVATE
    threeEdgeConnected
    sonLib
)