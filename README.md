-pedantic generates warnings on glew and glfw

C++11 is required for Dear ImGui
warning: anonymous variadic macros were introduced in C++11 [-Wvariadic-macros]

https://pyimgui.readthedocs.io/en/latest/guide/first-steps.html

## GLEW


glew-2.1.0

https://github.com/nigels-com/glew/releases/tag/glew-2.2.0

Build with CMake

        #        GIT_REPOSITORY https://github.com/nigels-com/glew.git
        # See https://github.com/nigels-com/glew/issues/291
        GIT_REPOSITORY https://github.com/Perlmint/glew-cmake.git   
        
                GIT_TAG glew-cmake-2.2.0
                # Don't use the glew-2.2.0 tag


## GLFW
https://www.glfw.org/download

Windows pre-compiled binaries

https://github.com/glfw/glfw/releases/download/3.3.2/glfw-3.3.2.bin.WIN64.zip

glfw-3.3.2.bin.WIN64