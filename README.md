---

# Python-GVAS-JSON-Converter

Python-GVAS-JSON-Converter (SavConverter) is a library designed to convert Unreal Engine's Game Variable and Attribute System (GVAS) files between `.sav` and `.json` formats. It provides a way to read and interpret the binary structure of `.sav` files and translate them into human-readable JSON format, as well as convert JSON back to the original `.sav` format.

## Update to UE5

- **File SavProperties**: Class `HeaderProperty` didn't read some bytes (int32) after reading engine build field. The length of the engine branch string was calculated incorrectly because of this. It was fixed by forced reading int32 bytes after engine build reading and named `engine_build_` because these bytes are still unknown. You can use `read_sav` and `sav_to_json` functions from author's library with modified `HeaderProperty` class clearly.

## Features

- **Convert from .sav to .json**: Supports converting Unreal Engine's `.sav` files into `.json` format.
- **Convert from .json to .sav**: Includes the ability to convert `.json` files back to the original `.sav` format.
- **JSON Editing Functions**: Offers a range of functions to navigate, manipulate, and modify the specific JSON structure with ease.
- **Tested Games**: The conversion has been tested with the following games (and may work for others):
  - **`Crab Champions`**
  - **`Deep Rock Galactic`**
  - **`High On Life`**
  - **`Hogwarts Legacy`**
  - **`Stray`**
- **Actively Developed**: This project is actively being developed, with new features and improvements being added.

## Warning

- **Untested .sav Files**: Some classes in [SavProperties.py](SavConverter/SavProperties.py) may not function correctly with untested `.sav` files, and certain [SavReader.py](SavConverter/SavReader.py) code segments may be broken for untested datatypes. While the library has been designed with flexibility in mind, full compatibility with all `.sav` files cannot be guaranteed at this stage. Efforts will continue to progressively test other games' `.sav` files and refine the code accordingly.

## Installation

To install SavConverter, you can use pip. Open your terminal and run the following command:

```shell
pip install SavConverter
```

This will install the latest version of SavConverter.

## Using the Conversion Functions

The conversion functions provide an easy way to translate between Unreal Engine's `.sav` and `.json` formats.

### Converting from .sav to .json

1. **Read .sav**: Use `read_sav(file_path)` to get the property instances from the `.sav` file.
2. **Convert to JSON**: Use `sav_to_json(props, string=True)` to convert properties to JSON. Use the `string` parameter to return a JSON string or object.
3. **Write to File**: Write the JSON string output to a `.json` file.

### Converting from .json to .sav

1. **Load JSON**: Use `load_json(file_path)` to read a JSON file.
2. **Convert to Binary**: Use `json_to_sav(json_string)` to convert JSON to binary data.
3. **Write to File**: Write the binary data to a `.sav` file.

## Using JSON Editing Functions

The JSON editing functions allow users to navigate and manipulate the JSON structure using paths, providing functions like:

### **Finding Objects**

- `get_object_by_path(data, path)`: Locate objects in JSON by specifying the path. Returns the object found at the specified path or `None` if the path is not found.

### **Inserting Objects**

- `insert_object_by_path(data, path, new_object, position='after')`: Add a new object at the specified location. Use the `position` parameter to insert before or after the targeted object.

### **Replacing Objects**

- `replace_object_by_path(data, path, new_object)`: Replace an object at the specified path with a new object.

### **Updating Properties**

- `update_property_by_path(data, path, new_value)`: Modify specific keys within an object at the given full path to the property.

### **Loading JSON**

- `load_json(file_path)`: Load a JSON file from the specified file path.

### **Converting Object to JSON String**

- `obj_to_json(obj)`: Convert an object into a JSON string with proper indentation.

### **Printing JSON**

- `print_json(data)`: Print a JSON object with indentation for better readability.

### Understanding the Path Structure

- `path`: A list that describes the path to the object you're looking for. Each element in the list can be:
  - **A dictionary**, to match a specific key-value pair.
  - **A string**, to reference a key.
  - **An integer**, to reference an index in a list.

Example path:
```python
path_to_find = [{"name": "RankedWeapons"}, "value", 0, {'name': 'Rank'}, 'value']
```
Let's break down the example path:

- `{"name": "RankedWeapons"}`: Look for an object with a key `"name"` and a value `"RankedWeapons"`.
- `"value"`: Inside the found object, look for the key `"value"`.
- `0`: Inside the value, look for the first element in the list (index `0`).
- `{'name':'Rank'}`: Look for an object within that element with a key `"name"` and a value `"Rank"`.
- `"value"`: Inside the found object, look for the key `"value"`.

This path leads you directly to a specific part of the JSON structure

## Example Code

A comprehensive usage example for all the available functions is provided in the [Example.py](Example.py) file. This example was developed using the `Crab Champions` `.sav` and `.json` files, which you can find in the [ExampleSavFiles](ExampleSavFiles) directory.

---
