# How to install MinGW64 with Cmake with Gtest
- ## Installing MinGW64 
        1- Go to "https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/seh/x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z"
        2- Download the Zip file ( if the link is not working go to "https://sourceforge.net/projects/mingw-w64/files/"  and scroll down to find x86_64-posix-seh)
        3- Exctract the Zip file , go to bin , take the bath copy   
        4- Go to Environmental variables on your Windows settings 
        5- edit the Path and add the path you copied from bin folder

- ## Installing Cmake
        1- Go to "https://cmake.org/download/" 
        2- Download and install , next ,next Mark add to PATH option
        3- If you marked add to PATH you don't have to take the bin file path and add it , it's automatically added :)

- ## Installing GTest
        1- Clone the repo and follow this video for better illustration :https://github.com/google/googletest
        https://www.youtube.com/watch?v=4RetR9-PDHE&t=7s



--------------------------------------------------------
# CMake Demo project
- ### CMakeLists.txt:
```CMakeLists.txt
cmake_minimum_required(VERSION 3.0)     #specfing the minimum version of cmake



project(MyProject)                          #specfing the project name



#finding the package of the googletest
find_package(GTest REQUIRED)           #finding the package of the googletest on the local machine


#debuging message 
message("Hoooooray GTest_FOUND: ${GTest_FOUND} ---> Found Done")  #printing the value of the GTest_FOUND

#this step is required to enable the C test for the files
enable_testing()                       #enabling the Ctesting in the project




#assiging the files to the variables
set(SRC_FILE calc.c)         #put the function you want to test here
set(TST_FILE test_calc.cpp)  #put the unit test code here


#adding the executable file to the project
add_executable(
    ${PROJECT_NAME}
    ${SRC_FILE}
    ${TST_FILE}
)



#static code
target_link_libraries(
    ${PROJECT_NAME}
    GTest::gtest
    GTest::gmock_main #required If we don't have amain code just the function.cpp

)


#makes the program knows which testfiles to take 
include(GoogleTest)
gtest_discover_tests(${PROJECT_NAME})

```
- ### Commands to run the Test:
```batch
1-mkdir build
2-cd build
3-cmake -G "MinGW Makefiles" ..
4- make -j
5- Runthe Exe file
```
