cmake_minimum_required(VERSION 3.10)
project(solver)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Основная программа
add_executable(solver solver.cpp)

# Тесты
enable_testing()
add_executable(test_solver tests/test_solver.cpp)
add_test(NAME SolverTest COMMAND test_solver)

# ========== CPACK НАСТРОЙКИ ==========
set(CPACK_PACKAGE_NAME "solver")
set(CPACK_PACKAGE_VERSION "0.1.0.0")
set(CPACK_PACKAGE_CONTACT "pavel@example.com")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Solver application for CPack demo")
set(CPACK_PACKAGE_DESCRIPTION_FILE "${CMAKE_CURRENT_SOURCE_DIR}/DESCRIPTION")
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/LICENSE")
set(CPACK_RESOURCE_FILE_README "${CMAKE_CURRENT_SOURCE_DIR}/README.md")

# Генераторы для всех платформ
set(CPACK_GENERATOR "DEB;RPM;TGZ;WIX;DragNDrop")

# ========== RPM НАСТРОЙКИ ==========
set(CPACK_RPM_PACKAGE_NAME "solver")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "Applications")
set(CPACK_RPM_PACKAGE_RELEASE 1)

# ========== DEB НАСТРОЙКИ ==========
set(CPACK_DEBIAN_PACKAGE_NAME "solver")
set(CPACK_DEBIAN_PACKAGE_PREDEPENDS "cmake >= 3.0")
set(CPACK_DEBIAN_PACKAGE_RELEASE 1)

# ========== WIX (MSI) НАСТРОЙКИ ==========
# Эти настройки нужны только для Windows сборки
if(WIN32)
    set(CPACK_WIX_UPGRADE_GUID "4E446239-5DDE-4D61-A122-D1D2F35F2112")
    set(CPACK_WIX_LICENSE_RTF "${CMAKE_CURRENT_SOURCE_DIR}/license.rtf")
    set(CPACK_WIX_MANUFACTURER "Pavel Dats")
    set(CPACK_WIX_PROPERTY_ARPURLINFOABOUT "https://github.com/PavelDats1/lab06")
endif()

# Установка программы
install(TARGETS solver RUNTIME DESTINATION bin)

# Подключение CPack
include(CPack)
