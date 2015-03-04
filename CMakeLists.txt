project(menda)
set(PROJECT_VERSION "20150303")

cmake_minimum_required(VERSION 2.8.12 FATAL_ERROR)

include(WriteBasicConfigVersionFile)
include(FeatureSummary)

find_package(ECM 0.0.11 REQUIRED NO_MODULE)
set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR})

find_package(KF5 ${KF5_MIN_VERSION} REQUIRED COMPONENTS Plasma)
  
include(ECMInstallIcons)
include(KDEInstallDirs)
include(KDECMakeSettings)
include(KDECompilerSettings)
include(GenerateExportHeader)

add_subdirectory(Menda)
add_subdirectory(wallpapers)

plasma_install_package(lookandfeel org.kde.menda.desktop look-and-feel lookandfeel)
  
install(DIRECTORY lookandfeel/contents/loginmanager/ DESTINATION ${CMAKE_INSTALL_PREFIX}/share/sddm/themes/menda PATTERN "README.txt" EXCLUDE)
install(DIRECTORY lookandfeel/contents/components DESTINATION ${CMAKE_INSTALL_PREFIX}/share/sddm/themes/menda PATTERN "README.txt" EXCLUDE)
    
INSTALL(FILES colors/Menda.colors DESTINATION ${DATA_INSTALL_DIR}/color-schemes/)
INSTALL(FILES colors/MendaDark.colors DESTINATION ${DATA_INSTALL_DIR}/color-schemes/)
if(EXISTS ${CMAKE_SOURCE_DIR}/po AND IS_DIRECTORY ${CMAKE_SOURCE_DIR}/po)
  find_package(KF5I18n CONFIG REQUIRED)
  ki18n_install(po)
endif()

feature_summary(WHAT ALL INCLUDE_QUIET_PACKAGES FATAL_ON_MISSING_REQUIRED_PACKAGES)
