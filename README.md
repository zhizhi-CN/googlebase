# googlebase
build chromium/src/base standalone

# 
DEPOT_TOOLS_WIN_TOOLCHAIN=0
# useage
    gclient config https://github.com/horatii/googlebase.git

    gclient sync  

    cd googlebase  

    gn gen out  

    ninja -C out googlebase  
