cmake_minimum_required(VERSION 3.29)

project(VulkanTutorial)

# Add CMake module path for FindVulkan.cmake if needed
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/CMake")

# Find required packages
find_package(glfw3 REQUIRED)
find_package(glm REQUIRED)
find_package(Vulkan REQUIRED)

# Create the executable from main.cpp
add_executable(VulkanTutorial main.cpp)

# Set C++ standard
set_target_properties(VulkanTutorial PROPERTIES CXX_STANDARD 20)

# Link libraries
target_link_libraries(VulkanTutorial 
    Vulkan::Vulkan 
    glfw
    glm::glm
)

# Define Vulkan-specific compile definitions
target_compile_definitions(VulkanTutorial PRIVATE 
    VULKAN_HPP_DISPATCH_LOADER_DYNAMIC=1
    VULKAN_HPP_NO_STRUCT_CONSTRUCTORS=1
)

# Set working directory for Visual Studio debugger
if(WIN32)
    if(${CMAKE_GENERATOR} MATCHES "Visual Studio.*")
        set_target_properties(VulkanTutorial PROPERTIES 
            VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_BINARY_DIR}")
    endif()
endif()