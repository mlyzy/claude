# JSON-C Installation and Testing Summary

This document summarizes the process of downloading, building, and testing the json-c library.

## 1. Introduction

JSON-C is a C library for parsing and manipulating JSON data. It implements a reference counting object model that allows you to easily construct JSON objects in C, output them as JSON formatted strings, and parse JSON formatted strings back into C representations. It aims to conform to [RFC 8259](https://www.rfc-editor.org/rfc/rfc8259).

## 2. Prerequisites Installation

First, we installed the necessary build tools:

```bash
sudo apt-get update && sudo apt-get install -y git build-essential cmake autoconf automake libtool
```

This command installs:
- `git`: For cloning the repository
- `build-essential`: Includes gcc, g++, and make
- `cmake`: The build system used by json-c
- `autoconf`, `automake`, `libtool`: Common build tools for C projects

## 3. Obtaining the Source Code

We cloned the json-c repository from GitHub:

```bash
git clone https://github.com/json-c/json-c.git
```

This command:
- Downloads the latest version of json-c from the official GitHub repository
- Creates a local copy in the `json-c` directory

## 4. Building the Library

We created a build directory and used CMake to configure and build the project:

```bash
mkdir json-c-build
cd json-c-build
cmake ../json-c
make
```

These commands:
1. Create a separate build directory to keep build artifacts separate from source
2. Change to the build directory
3. Run CMake to generate the build files from the source directory
4. Execute make to compile the source code into libraries and executables

The build process:
- Compiled the core json-c library as both static (`libjson-c.a`) and shared (`libjson-c.so`) libraries
- Built test executables for verifying the library's functionality
- Built example applications, including the `json_parse` utility

## 5. Running Tests

We ran the test suite to verify that the library works correctly:

```bash
make test
```

This command:
- Ran a total of 25 tests covering different aspects of the library
- All tests passed, confirming that the library functions as expected

Test results showed:
- 25/25 tests passed
- Test categories included object manipulation, parsing, serialization, and value handling
- The tests completed in a fraction of a second

## 6. Testing with the Example Application

We tested the built-in `json_parse` utility to verify practical functionality:

```bash
./json_parse -f ~/test.json
```

This command:
- Used the json_parse utility with the `-f` flag to format the output
- Successfully parsed our test JSON file
- Displayed the formatted JSON content

Our test JSON file contained:
```json
{
  "name": "json-c test",
  "version": 1.0,
  "features": ["parsing", "serialization", "tree manipulation"],
  "metrics": {
    "performance": "good",
    "memory": "efficient"
  },
  "active": true
}
```

## 7. Writing a Custom Test Program

We created a custom C program to demonstrate using the json-c library:

```c
#include <stdio.h>
#include <json_object.h>
#include <json_tokener.h>
#include <json_util.h>

int main() {
    // Create a new JSON object
    struct json_object *root = json_object_new_object();
    
    // Add a string
    json_object_object_add(root, "name", json_object_new_string("json-c example"));
    
    // Add a number
    json_object_object_add(root, "version", json_object_new_double(1.0));
    
    // Create and add an array
    struct json_object *features = json_object_new_array();
    json_object_array_add(features, json_object_new_string("easy to use"));
    json_object_array_add(features, json_object_new_string("lightweight"));
    json_object_array_add(features, json_object_new_string("fast"));
    json_object_object_add(root, "features", features);
    
    // Create and add a nested object
    struct json_object *metrics = json_object_new_object();
    json_object_object_add(metrics, "performance", json_object_new_string("excellent"));
    json_object_object_add(metrics, "footprint", json_object_new_string("small"));
    json_object_object_add(root, "metrics", metrics);
    
    // Add a boolean
    json_object_object_add(root, "stable", json_object_new_boolean(1));
    
    // Print the JSON with different formatting options
    printf("JSON_C_TO_STRING_PLAIN:\n%s\n\n", 
           json_object_to_json_string_ext(root, JSON_C_TO_STRING_PLAIN));
    
    printf("JSON_C_TO_STRING_PRETTY:\n%s\n\n", 
           json_object_to_json_string_ext(root, JSON_C_TO_STRING_PRETTY));
    
    printf("JSON_C_TO_STRING_SPACED:\n%s\n\n", 
           json_object_to_json_string_ext(root, JSON_C_TO_STRING_SPACED));
    
    // Access specific elements
    struct json_object *name_obj;
    json_object_object_get_ex(root, "name", &name_obj);
    printf("Name: %s\n", json_object_get_string(name_obj));
    
    struct json_object *features_obj;
    json_object_object_get_ex(root, "features", &features_obj);
    printf("Features count: %d\n", json_object_array_length(features_obj));
    
    struct json_object *first_feature = json_object_array_get_idx(features_obj, 0);
    printf("First feature: %s\n", json_object_get_string(first_feature));
    
    // Clean up (decrements reference count)
    json_object_put(root);
    
    return 0;
}
```

We compiled and ran this program:

```bash
gcc -o json_test json_test.c -I/home/computeruse/json-c -I/home/computeruse/json-c-build -L/home/computeruse/json-c-build -ljson-c
LD_LIBRARY_PATH=/home/computeruse/json-c-build ./json_test
```

These commands:
1. Compiled our C program with appropriate include and library paths
2. Set the library path to include our build directory
3. Executed the program

The program demonstrated:
- Creating JSON objects, arrays, and nested structures
- Adding different data types (strings, numbers, booleans)
- Serializing JSON with different formatting options
- Accessing specific elements within the JSON structure
- Proper memory management with reference counting

## 8. Conclusion

We successfully installed, built, and tested the json-c library. The library provides a robust API for handling JSON data in C applications, with features including:

- Creation and manipulation of JSON objects
- Parsing JSON text into object structures
- Serializing objects back to JSON text with various formatting options
- Accessing and modifying JSON data elements
- Memory management through reference counting

The built library provides both static and shared library options, and the tests confirm its proper functionality.
