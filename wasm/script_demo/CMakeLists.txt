SET(CMAKE_EXECUTABLE_SUFFIX ".html")
SET(EXE_NAME osgVerse_JsCallerWASM)
SET(EXECUTABLE_FILES
    ccall_viewer.h ccall_viewer.cpp
)

SET(WASM_FLAGS3 "-s EXPORTED_RUNTIME_METHODS=\"['cwrap']\" --post-js ${CMAKE_CURRENT_SOURCE_DIR}/caller.js")
NEW_EXECUTABLE(${EXE_NAME} SHARED)
SET_TARGET_PROPERTIES(${EXE_NAME} PROPERTIES LINK_FLAGS
                      "${WASM_FLAGS0} ${WASM_FLAGS1} ${WASM_FLAGS2} ${WASM_FLAGS3} ${WASM_FLAGS_EX}")

SET_PROPERTY(TARGET ${EXE_NAME} PROPERTY FOLDER "APPLICATIONS")
TARGET_LINK_LIBRARIES(${EXE_NAME} osgVerseDependency osgVerseAnimation osgVerseReaderWriter
                      osgVersePipeline osgVerseScript osgVerseWrappers)
LINK_OSG_LIBRARY(${EXE_NAME} OpenThreads osg osgDB osgUtil osgGA osgText osgSim osgTerrain osgViewer)
TARGET_COMPILE_OPTIONS(${EXE_NAME} PUBLIC -D_SCL_SECURE_NO_WARNINGS)
