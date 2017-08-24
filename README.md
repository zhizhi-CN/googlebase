# googlebase
build chromium/src/base standalone

# useage
`
    gclient config https://github.com/horatii/googlebase.git
    gclient sync
    cd googlebase
    gn gen out
    ninja -C out googlebase
`
