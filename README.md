# Chart Generator – Software Design Case Study

This project is a software design case study for a command-line chart generation system.
The focus is on requirements analysis, UML modeling, and design improvements using
SOLID principles, cohesion, and coupling.

## Overview
The system takes structured data (JSON, YAML) and generates charts (line, scatter)
exported to formats such as SVG or PDF. The design emphasizes modular subsystems
and extensibility.

## What I Did
- Created use cases and a use case diagram based on system requirements
- Designed a full UML class diagram representing system architecture
- Created four sequence diagrams covering key workflows
- Analyzed cohesion and coupling across subsystems
- Applied SOLID principles and design patterns (Strategy, Builder)

## Subsystems
- **Input Subsystem**: Parses input files into a DataSet
- **Chart Generation Subsystem**: Converts DataSet into a ChartModel
- **Output Subsystem**: Renders charts into output formats

## Key Design Decisions
- Used abstraction and dependency inversion to reduce coupling
- Applied Builder pattern for chart construction
- Used Strategy-style selection for parsers and renderers
- Centralized coordination in a controller class

## Files
- Use cases and diagrams are provided as yUML and Mermaid sources
- Design improvement analysis is documented in `design-improvements.md`

## Notes
This repository contains only design artifacts created by the team and does not
include course starter code or instructor materials.
