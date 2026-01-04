# Chart Generator

> I want a system that will generate different types of charts from supplied data.  The data may be in any number of formats including JSON and YAML.  From the data, it will generate a line chart or scatterplot, possibly others.  Charts should be able to be output into different image formats such as SVG or PDF.

**Notes**

* A command-line utility is desired, with chart type and 
* Users will specify what kind of chart is generated
* Users give data through file, assumed to have valid input, if desired
* Output is always to a file

## Use Cases

### Generate Chart from User Input

#### Main Success Scenario
1. User specifies input data file path, chart type, output image format, and destination file path when running the program.
2. System validates and parses these options
3. System reads and parses the input file into an internal dataset (includes Read Input Data File)
4. System validates the data set and builds a chart model for the selected chart type (includes Build Chart Model)
5. System renders the chart model and writes an image file in the requested format to the destination (includes Render Image File)
6. System exits successfully

#### Extension
1a. User runs the system with --help or no arguments
  2. System displays instructions and exits
  
2a. Invalid or missing arguments
  2. System prints an error message and exits

3a. File path is unreadable or invalid
  2. System prints an error message and exits

4a. Data is not compatible with the chart type
  2. System prints an error message and exits

5a. Output format is not supported, or the destination path is invalid
  2. System prints an error message and exits

### Read Input Data File

#### Main Success Scenario
1. System opens the user's input file at the given path
2. System validates the format of the input data (e.g., JSON, YAML, or other supported formats)
3. System parses the file content into an internal dataset stored in memory for future use

### Extensions
1a. File not found or unreadable
  2. System prints an error message and exits

2a. File format not recognized or unsupported
  2. System prints an error message and exits

3a. Invalid or corrupted data structure
  2. System prints an error message and exits
  
### Build Chart Model

#### Main Success Scenario
1. System checks dataset compatibility with the user's selected chart type (such as valid fields for line, scatter, etc.)
2. System maps fields (e.g., x, y, series) and applies defaults/options (axes, labels, scales, legend)
3. System constructs an internal chart model that is prepared for rendering

#### Extensions
1a. Required fields missing or invalid for chart type
  2. System prints an error message and exits

2a. The dataset is too large
  2. System prints an error message and exits

### Render Image File

#### Main Success Scenario
1. System converts the chart model to the user's specified output image format (e.g., SVG, PDF, or other supported formats)
2. System writes the rendered chart to the destination output path
3. System confirms successful generation and exits

#### Extensions
1a. Output format not supported
  2. System prints an error message and exits

2a. Invalid destination path
  2. System prints an error message and exits

## Use Case Diagram
![Use Case Diagram](http://yuml.me/e0f3af9e.svg)

## Class Diagram
![Class Diagram](https://yuml.me/5675c190.svg)

[//]: # (Editable link: http://yuml.me/edit/5675c190)

## Sequence Diagram
### Read Input Data File:

<img width="2108" height="982" alt="image" src="https://github.com/user-attachments/assets/ac199c6d-9712-49f4-b078-5479a894fa2e" />

### Building an Internal Chart Representation

<img width="1864" height="882" alt="image" src="https://github.com/user-attachments/assets/66c4fb45-da08-412b-a09d-7f4f13c88119" />

### Render Image File

<img width="1656" height="702" alt="image" src="https://github.com/user-attachments/assets/156ec197-8704-4d4f-a516-031c2279ca6c" />

### Generate Chart from User Input

<img width="3798" height="1602" alt="image" src="https://github.com/user-attachments/assets/99fc6bba-b338-42ed-94f3-0cdc1fe973b7" />
