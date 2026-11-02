cmake_minimum_required(VERSION 3.20)

project(swim_animator_shore VERSION 0.1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(SHORE_BUILD_EXAMPLES OFF)
set(SHORE_BUILD_TESTS OFF)
add_subdirectory(
    "${CMAKE_CURRENT_SOURCE_DIR}/../shore"
    "${CMAKE_CURRENT_BINARY_DIR}/shore"
)

find_package(wxWidgets REQUIRED COMPONENTS core base aui xml)
include("${wxWidgets_USE_FILE}")

set(SWIM_ANIMATOR_SOURCES
    src/App.cpp
    src/MainFrame.cpp
    src/Document.cpp
    src/View.cpp
    src/DrawDoc.cpp
    src/DrawView.cpp
    src/DrawCommands.cpp
    src/PropPanel.cpp
    src/Palette.cpp
    src/ColorSwatchPanel.cpp
    src/SpaDoc.cpp
    src/SpaView.cpp
    src/SpaSaveAsDialog.cpp
    src/AssetManagerPanel.cpp
    src/NewDrawingDialog.cpp
    src/HierarchyPanel.cpp
    src/SnapSettings.cpp
    src/SnapEngine.cpp
    src/SettingsDialog.cpp
    src/SmilTypes.cpp
    src/SmilDoc.cpp
    src/SmilView.cpp
    src/ScenePanel.cpp
    src/KeyframePanel.cpp
    src/CollapseManager.cpp
)

add_executable(swim-animator WIN32 MACOSX_BUNDLE ${SWIM_ANIMATOR_SOURCES})
target_include_directories(swim-animator PRIVATE src)
target_link_libraries(swim-animator PRIVATE shore ${wxWidgets_LIBRARIES})

set_target_properties(swim-animator PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER "se.swimanimator.shore"
    MACOSX_BUNDLE_BUNDLE_VERSION "${PROJECT_VERSION}"
    MACOSX_BUNDLE_SHORT_VERSION_STRING "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}"
)
