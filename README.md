# BMAD Requirements Analyzer Agent - Setup Guide

**Created:** 13 November 2025
**Version:** 1.0
**Author:** BMAD Requirements Analyzer Agent

This guide documents the complete process of creating and using the BMAD Requirements Analyzer Agent to generate Mermaid diagrams from system requirements.

## 📋 Table of Contents

- [Overview](#overview)
- [What We Built](#what-we-built)
- [Prerequisites](#prerequisites)
- [Step 1: Create the Agent](#step-1-create-the-agent)
- [Step 2: Compile the Agent](#step-2-compile-the-agent)
- [Step 3: Use the Agent](#step-3-use-the-agent)
- [Step 4: Save Diagrams](#step-4-save-diagrams)
- [Diagram Examples](#diagram-examples)
- [Troubleshooting](#troubleshooting)
- [File Structure](#file-structure)

## 🎯 Overview

This guide shows how to create a BMAD agent that analyzes system requirements and automatically generates professional Mermaid diagrams. The agent can create flowcharts, sequence diagrams, class diagrams, and more.

## 🏗️ What We Built

### Requirements Analyzer Agent
- **Purpose**: Analyzes requirements and generates Mermaid diagrams
- **Capabilities**:
  - Requirements analysis and breakdown
  - Multiple diagram types (flowchart, sequence, class)
  - Automatic diagram generation
  - File saving to workspace
- **Location**: `bmad/agents/requirements-analyzer.agent.yaml`

### Generated Diagrams
1. **Ecommerce Flowchart** - Complete customer journey
2. **Authentication Sequence** - Security system flow
3. **Multiple Formats** - Mermaid code, Draw.io integration

## 📋 Prerequisites

- BMAD-METHOD framework installed
- Node.js and npm
- Draw.io (optional, for diagram editing)
- Basic understanding of YAML and Mermaid syntax

## 🚀 Step 1: Create the Agent

### 1.1 Create Agent YAML File

Create the file `bmad/agents/requirements-analyzer.agent.yaml` with this content:

```yaml
# Requirements Analyzer
# Expert agent for analyzing requirements and generating Mermaid diagrams
# Module: Standalone

agent:
  metadata:
    id: bmad/agents/requirements-analyzer.md
    name: Requirements Analyzer
    title: Requirements Analysis Expert
    icon: 📊
    module: agents
    type: expert

  persona:
    role: |
      Requirements Analysis and Diagram Generation Specialist - Expert in breaking down complex requirements into clear, visual representations.

    identity: |
      Specialized analyst with deep expertise in requirements engineering, system analysis, and visual modeling. I transform textual requirements into structured diagrams that reveal system architecture, data flows, and business processes. My diagrams serve as blueprints for development teams, ensuring everyone understands the system from the same perspective.

    communication_style: |
      Analytical Expert - Systematic, data-driven, hierarchical. I approach requirements with methodical precision, breaking down complex systems into understandable components. I explain my analysis clearly and provide diagrams that speak for themselves.

    principles:
      - I believe in thorough analysis before visualization - understanding comes before representation
      - I ensure diagrams accurately reflect the requirements without adding assumptions
      - I choose the most appropriate diagram type for each requirement set
      - I provide clear explanations of diagram structure and meaning
      - I maintain consistency in notation and style across related diagrams
      - I focus on clarity and readability for all stakeholders

  critical_actions:
    - Load into memory {project-root}/bmad/bmb/config.yaml and set variables
    - Remember the users name is {user_name}
    - ALWAYS communicate in {communication_language}
    - When generating diagrams, always output valid Mermaid syntax
    - Ask for clarification when requirements are ambiguous

  menu:
    - trigger: analyze-requirements
      action: |
        I'll analyze your requirements text. Please provide the requirements document or paste the text here.
        I'll identify key components, processes, entities, and relationships, then generate an appropriate Mermaid diagram.
        The diagram will be saved to {output_folder}/diagrams/requirements-diagram.md
      description: Analyze requirements text and generate Mermaid diagram

    - trigger: generate-flowchart
      action: |
        Let's create a flowchart diagram. Describe the process or workflow you want to visualize,
        including steps, decisions, and flows. I'll generate the Mermaid flowchart code and save it to {output_folder}/diagrams/flowchart.md
      description: Generate a Mermaid flowchart from process description

    - trigger: generate-sequence
      action: |
        For sequence diagrams, I need to know the actors/participants and the sequence of interactions.
        Provide the scenario or use case, and I'll create the Mermaid sequence diagram and save it to {output_folder}/diagrams/sequence-diagram.md
      description: Generate a Mermaid sequence diagram

    - trigger: generate-class
      action: |
        Class diagrams show the structure of systems. Provide information about classes, their properties,
        methods, and relationships (inheritance, composition, etc.), and I'll generate the diagram and save it to {output_folder}/diagrams/class-diagram.md
      description: Generate a Mermaid class diagram

    - trigger: help
      action: |
        I can help you analyze requirements and generate various types of Mermaid diagrams:
        - Flowcharts for processes and workflows
        - Sequence diagrams for interactions
        - Class diagrams for system structure
        - Entity-relationship diagrams for data models
        Just provide your requirements or describe what you want to visualize!
        All generated diagrams are automatically saved to {output_folder}/diagrams/
      description: Show help and available diagram types
```

### 1.2 Agent Features

The agent includes:
- **Expert persona** with analytical communication style
- **Multiple diagram types** support
- **Automatic file saving** to workspace
- **Requirements analysis** capabilities
- **Help system** for guidance

## 🔧 Step 2: Compile the Agent

### 2.1 Run BMAD Installation

Compile the agent using the BMAD CLI:

```bash
npm run install:bmad
```

This will:
- Compile the YAML agent to executable MD format
- Update the agent registry
- Make the agent available for use

### 2.2 Verify Compilation

Check that these files were created:
- `bmad/agents/requirements-analyzer.md` (compiled agent)
- `docs/diagrams/` (output directory)

## 🎨 Step 3: Use the Agent

### 3.1 Activate the Agent

In your BMAD environment, activate the Requirements Analyzer agent.

### 3.2 Generate Diagrams

Use these commands:

#### Analyze Requirements
```
*analyze-requirements
```
Provide your requirements text, and the agent will:
- Analyze the requirements
- Identify key components and flows
- Generate appropriate diagram type
- Save to `docs/diagrams/requirements-diagram.md`

#### Generate Specific Diagram Types
```
*generate-flowchart
*generate-sequence
*generate-class
```

Each command will prompt for input and save the diagram to the appropriate file.

#### Get Help
```
*help
```
Shows available commands and diagram types.

## 💾 Step 4: Save Diagrams

### 4.1 Automatic Saving

The agent automatically saves diagrams to:
```
docs/diagrams/
├── requirements-diagram.md
├── flowchart.md
├── sequence-diagram.md
├── class-diagram.md
└── *.mmd (Mermaid files)
```

### 4.2 Draw.io Integration

#### Option A: Import Mermaid Files
1. Open Draw.io
2. File → Import → Mermaid...
3. Select `.mmd` file from `docs/diagrams/`
4. Diagram renders automatically

#### Option B: Direct Draw.io Format
For direct Draw.io integration:
1. Create a basic `diagram.drawio` file
2. Use the agent to generate Draw.io XML format
3. Replace the diagram content

### 4.3 Manual Mermaid Files

Create `.mmd` files for Draw.io import:

```bash
# Save as auth-sequence.mmd
sequenceDiagram
    participant U as User
    participant AS as Auth Server
    # ... diagram content
```

## 📊 Diagram Examples

### Ecommerce Flowchart
```
flowchart TD
    A[User Visits Store] --> B{Logged In?}
    B -->|No| C[User Registration/Login]
    B -->|Yes| D[Browse Products]
    # ... complete flowchart
```

### Authentication Sequence
```
sequenceDiagram
    participant U as User
    participant AS as Auth Server
    U->>AS: POST /login
    AS->>AS: Verify credentials
    AS-->>U: Return JWT token
```

## 🔧 Troubleshooting

### XML Parsing Errors in Draw.io
**Error:** "Not a diagram file (error on line X at column Y: xmlParseEntityRef: no name)"

**Solution:** Encode special characters properly
- `&` → `&amp;`
- `•` → `&#8226;`
- `→` → `&#8594;`
- Remove emojis (🔒 📝)

### Agent Not Found
**Error:** Agent commands not recognized

**Solution:**
1. Verify agent compilation: `npm run install:bmad`
2. Check file exists: `bmad/agents/requirements-analyzer.md`
3. Restart BMAD environment

### Diagrams Not Saving
**Error:** Files not created in `docs/diagrams/`

**Solution:**
1. Check output folder configuration in `bmad/bmb/config.yaml`
2. Ensure write permissions on `docs/` directory
3. Verify agent has file saving actions configured

### Mermaid Syntax Errors
**Error:** Invalid Mermaid code

**Solution:**
- Use correct Mermaid syntax
- Validate at mermaid.live
- Check for missing semicolons or brackets

## 📁 File Structure

After setup, your project should have:

```
BMAD-METHOD/
├── bmad/
│   ├── agents/
│   │   └── requirements-analyzer.agent.yaml  # Source
│   │   └── requirements-analyzer.md          # Compiled
│   └── bmb/
│       └── config.yaml                        # Configuration
├── docs/
│   └── diagrams/                              # Output directory
│       ├── requirements-diagram.md
│       ├── flowchart.md
│       ├── sequence-diagram.md
│       ├── class-diagram.md
│       └── *.mmd                             # Mermaid files
└── Test.drawio                               # Draw.io integration
```

## 🎯 Next Steps

1. **Test the Agent**: Try generating a diagram with sample requirements
2. **Customize**: Modify agent persona or add new diagram types
3. **Integrate**: Use in your development workflow
4. **Extend**: Add new analysis capabilities

## 📞 Support

- Check agent help: `*help`
- Verify compilation logs
- Test with simple requirements first
- Use mermaid.live for syntax validation

---

**Generated by BMAD Requirements Analyzer Agent**
**Date:** 13 November 2025
**Purpose:** Complete setup and usage guide for requirements analysis and diagram generation</content>
<parameter name="filePath">/Users/disandup/Desktop/New Template Drawio/BMAD-METHOD/REQUIREMENTS-ANALYZER-README.md
