# Project #2: Design Improvements

## Cohesion and Coupling
**Input Subsystem**

*Cohesion*

The Input Subsystem is highly cohesive because all of the behavior supports a single work flow, which is converting an input file path into a valid DataSet.
- ChartGenController provides a file path to DataParser
- The DataParser figures out which concrete parser should handle the file format
- JSONParser or YAMLParser then parses the contents of the file and returns a DataSet
- The DataSet stores the parsed record and state, then it is passed to the next subsystem.

Each step in this flow supports the same responsibility and none of the steps perform unrelated work such as chart builder or rendering. Due to all the classes participating in the same workflow and not mixing responsibilities, the Input Subsystem is highly cohesive.

*Coupling*

The Input Subsystem has low coupling because its dependencies are minimal and abstracted.
- ChartGenController depends only on the abstract DataParser instead of choosing the JSONParser or YAMLParser
- Other subsystems interact with the Input Subsystem only through using the DataSet object, not through parsing logic or file structure
- The only data that goes into the input is the filePath and the DataSet is used for the output, which prevents high types of coupling
- Changes to the parser behavior will not require changes in chart generation or output

Since the dependencies of the subsystem are limited and abstract, it shows that it is low coupling.


**Chart Generation Subsystem**

*Cohesion*

The ChartGeneration Subsystem is highly cohesive because all of its classes and methods are focused on a single responsibility which is converting a valid DataSet into a ChartModel.
- The abstract ChartmodelBuilder only focuses on building a chart from a DataSet
- LineChartBuilder and ScatterChartBuilder only implement logic specific to their chart type and do not parse or render anything
- All the operations in this subsystem directly relate to chart construction, such as choosing a chart type, mopping data fields, and creating the internal chart
- ChartModel encapsulates chat data (axes, labels), which keeps all chart representation concerns inside the subsystem

Since the responsibilities are closely focused and not blended with input or output concerns, the Chart Generation Subsystem is highly cohesive

*Coupling*

The Chart Generation Subsystem has a low to medium couple because it interacts with other subsystems only through shared objects, while still depending on them for input and output.
- Builders depend only on the DataSet abstraction and do not depend on how input data was parsed or validated
- ChartGenController interacts with the subsystem through the abstract ChartModelBuilder, so it does not need to know which concrete builder is used
- The subsystem produces a ChartModel, which is the only dependency required by the Output Subsystem

Coupling is not completely low because the builders rely on the structure of DataSet and ChartModel. This dependency still works because these are shared objects instead of implementations. The coupling still stays controlled and does not tightly combine the subsystems to others.


**Output Subsystem**

*Cohesion*

The Output Subsystem is highly cohesive because all of its behavior supports a single responsibility, which is converting a ChartModel into an output file.
- ChartGenController provides a ChartModel and a destination path to the output subsystem
- ChartRenderer defines the abstract behavior for rendering a chart
- SVGRenderer and PDFRenderer only handle the logic that is needed to render the chart in their specific formats
- All methods in this subsystem are related to rendering and writing output and do not include parsing or chart construction

Because every class in this subsystem only relies on rendering, the Output Subsystem is highly cohesive.

*Coupling*

The Output Subsystem has low coupling because it interacts with the rest of the system only through the ChartModel and an output path.
- Renderers do not depend on how input data was parsed or how the chart was built
- ChartGenController interacts with the subsystem through the abstract ChartRenderer and does not depend on concrete renderers such as SVGRenderer or PDFRenderer
- Changes to rendering logic or output formats stay isolated inside of the Output Subsystem

This keeps dependencies minimal and prevents changes from affecting other subsystems.


**Systemwide**

*Cohesion*

The system as a whole is highly cohesive because all subsystems contribute to a single overall workflow, which is generating a chart image from input data.
- The Input Subsystem focuses on parsing data into a DataSet
- The Chart Generation Subsystem focuses on converting the DataSet into a ChartModel
- The Output Subsystem focuses on rendering the ChartModel into a final output format

Each subsystem performs a distinct step in the same process without overlapping responsibilities, which makes the systemwide design cohesive.

*Coupling*

The systemwide design has low coupling because subsystems interact only through shared domain objects and abstract classes.
- Subsystems exchange data using DataSet and ChartModel rather than accessing internal logic
- Everything is coordinated through ChartGenController, which depends on abstractions instead of classes being concrete
- No subsystem directly depends on the internal behavior of another subsystem

Because dependencies are limited and well defined, changes in one subsystem do not tightly affect the others, keeping coupling low across the system.



## Issues Fixed in Project #1

* **Fixed bad file naming**. Auxiliary files for the diagram sources are renamed and include file names.
* **Fully reorganized and rewrote use cases**. Reorganized use cases to more accurately reflect desired system and user interaction. Redrew the use case diagram in accordance with the new use cases.
* **Redrew class and sequence diagrams**, improving coherence with use cases. 
  

## SOLID Principles and Design Patterns Applied 

**Input Subsystem:**

Our input subsystem uses the Single Responsibility Principle, the Open/Closed Principle, and the Dependency Inversion Principle. It follows SRP because its only responsibility is parsing input files into a DataSet. The parsing logic is kept inside DataParser and its concrete implementations. This makes sure that the other responsibilities, such as chart generation and rendering, are handled by different subsystems. It uses OCP because new file formats can be supported by adding new parser classes without changing existing code that uses DataParser. The controller and other subsystems continue to interact with the parser through the same interface and still receive a DataSet. Lastly, DIP is only applied because ChartGenController depends on the abstract DataParser instead of the JSONParser or YAMLParser as shown in the class diagram. This makes sure that the file format handling only stays inside the specific parsers and can make parsers get changed without affecting ChartGenController.

**Chart Generation Subsystem**

In this subsystem, it uses the builder design pattern to create chart models from a DataSet. The abstract ChartModelBuilder defines the kind of build it needs, and the details get handled in LineChartBuilder and ScatterChartBuilder depending on the specific chart type. Each builder takes a DataSet and produces a ChartModel. This approach is used instead of using Factory because chart generation requires a creation process that varies by chart type, not just choosing which object to create. This follows the Dependency Inversion Principle because ChartGenController depends on the abstract ChartModelBuilder instead of the specific builder classes, which allows different chart types to be used without changing ChartGenController.

**Output Subsystem**

The output subsystem is very similar to the input subsystem with how it uses SOLID design as it follows the Single Responsibility Principle, the Open/Closed Principle, and the Dependency Inversion Principle. The way it uses SRP is that SVGRenderer and PDFRenderer are only responsible for rendering a chart into its specific output format. This makes sure the responsibilities are only focused on one objective and it does not have multiple output behaviors inside of one class. The abstract ChartRenderer defines the rendering behavior and can make newly added output formats by creating new renderer classes without changing the existing code. DIP is used because the abstract ChartRenderer has concrete renderer implementations that ChartGenController does not directly depend on. It only cares about the abstract class and it does not need to know how the rendering happens, it only cares about the output, which keeps rendering logic to be focused within its subsystem.

**Systemwide**

Throughout the entire system, the strategy design pattern is mainly used by letting the controller call each class, and the specific implementation for parsing, chart generation, and rendering is based on the user input or data type. This system can choose between different strategies such as the parser, chart builder, and renderers and keeps the overall workflow consistent instead of only coding a single approach. The Liskov Substitution Principle is used throughout the design because when an abstract class is used (like DataParser, ChartModelBuilder, or ChartRenderer), any concrete subclass can be substituted without affecting the accuracy. Each subclass takes the same input types and produces the expected output, which can allow them to be swapped whenever inside of the overall system. With all of these principles and design patterns, the system is very flexible and can be extended very easily without needing changes about the behavior.
