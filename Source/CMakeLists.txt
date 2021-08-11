set(APPLICATION_SOURCE_FILES
    "Application/Main.cpp"
    "Application/Application.cpp")

add_executable("Application" ${APPLICATION_SOURCE_FILES})
target_compile_features("Application" PRIVATE cxx_std_17)
target_link_libraries("Application" fmt::fmt)
