# Ideation and Concept Generation

## Team Members

Ethan Peterson, Siddhant Kulkarni, Kevin Shah, Sanjit Selvakumar

---

## Objective

The purpose of this assignment is to generate innovative design features for our product and present alternative versions that align with the project requirements. This brainstorming process is aimed at ensuring that we develop a solution that is both effective and adaptable.

---

## Project Description

This project involves designing a modular system that utilizes UART communication between independently developed subsystems. Each team member is responsible for creating a surface-mount PCB, and the integrated system must function seamlessly for the Innovation Showcase. Key considerations include individual contributions, collaborative teamwork, and strict adherence to technical requirements such as microcontroller specifications, ECAD tool usage, and the daisy-chain communication protocol. Success will be defined by effective planning, thorough testing, and compliance with integration and documentation standards.

---

## Science Exhibit Intentions

### Exhibit Goal

- Demonstrate meteorological data collection principles.
- Educate students on environmental sensors and cause-effect relationships in weather systems.
- Provide interactive, hands-on learning experiences.

### Target Audience

- K–12 students (ages ~6–16).
- Must support diverse learning styles and physical/cognitive capabilities.
- Accessible for younger students and enriching for older students.

---

## Key Design Considerations

- **Ease of Use**: Visual and tactile cues, textured buttons, intuitive layout.
- **Interactive Controls**: Touchscreen with drag-and-drop features, large push buttons.
- **Durability and Safety**: Robust materials, emergency stop, insulated wiring.
- **Instructional Design**: Clear diagrams, on-device instructions, optional tutorials.
- **Avoiding Pitfalls**:
  - Limit cognitive overload.
  - Gather and incorporate user feedback.
  - Maintain consistent theme and concept.

---

## Brainstorming Process

[Ideation Slides](https://docs.google.com/presentation/d/1-jR1jT5JZCxH_XFAIzBFzMHgu-b0iQvdZxi1QXmcdSc/edit)

- Organized ideas into four STEM categories:
  - Physics & Engineering
  - Chemistry & Materials
  - Biology & Life Sciences
  - Earth & Space Sciences
- Prioritized based on feasibility and educational impact.
- Selected top concepts for deeper evaluation.

### Brainstorming Figures

![Figure 1.1: Group of All Ideas](https://github.com/user-attachments/assets/1e00de76-5686-465f-b138-50225f9b2257)

*Figure 1.1: Group of All Ideas*

![Figure 1.2: Remaining Brainstormed Ideas](https://github.com/user-attachments/assets/3b4b366b-1fe7-4888-9008-b8bff55f9f06)

*Figure 1.2: Remaining Brainstormed Ideas*

![Figure 1.3: Physics & Engineering](https://github.com/user-attachments/assets/5323e01a-194b-4e6a-bae6-79369f9c7c50)

*Figure 1.3: Physics & Engineering*

![Figure 1.4: Chemistry & Materials Science](https://github.com/user-attachments/assets/4efae097-51d8-4c32-afc8-e6fd8f5d637b)

*Figure 1.4: Chemistry & Materials Science*

![Figure 1.5: Biology & Life Sciences](https://github.com/user-attachments/assets/d05eb711-f997-4e66-866b-5d0b22dbb364)

*Figure 1.5: Biology & Life Sciences*

![Figure 1.6: Earth & Space Science](https://github.com/user-attachments/assets/f15dccd1-fe54-4295-9df9-29adfab7508f)

*Figure 1.6: Earth & Space Science*

---

## Concept Sketches

![Figure 5.1](https://github.com/user-attachments/assets/c6580f80-2849-43cd-b637-b025bacc0ccb)

*Figure 5.1 - AI-Generated Representation of Project*

![Figure 5.2](https://github.com/user-attachments/assets/e3a333c3-b451-4b26-abd6-c3ed7dca48a6)

*Figure 5.2 - Overview of Weather Data Collection System*

---

## Science Exhibit Implementation

The Weather Data Collection System (WDC) is designed as an interactive exhibit that introduces K-12 students to meteorology through real-time sensor data visualization. The system integrates:

- ESP32 and PIC18F47Q10 microcontrollers
- I2C LCD display
- DHT11 (temp/humidity) and BMP180 (pressure) sensors

**Key Features:**
- **Intuitive LCD display** driven by I2C for weather feedback
- **Tactile buttons** for engaging with the data
- **Interactive mapping** of button-to-function
- **Safe and durable** enclosure for all-age use
- **Clear instructional cues** near controls

The design adheres to accessibility principles outlined in the “Suggested Guidelines for Designing Interactive Exhibits,” emphasizing visibility, safety, and cognitive simplicity. Safety is ensured through insulated components and ergonomic construction.

---

## Final Design Selection Process

The team used a criteria-based evaluation process focused on:
- Educational effectiveness
- Technical feasibility
- Interactivity
- Modularity

We merged the best ideas from initial brainstorming and eliminated infeasible elements. The selected concept—a real-time weather monitoring system—was chosen due to its STEM relevance, modular hardware-software integration, and user-friendly design.

---

## How This Led to an AC System Concept

As the design matured, real-world constraints and technical challenges shifted our direction. Key insights included:

- **Incorporated**: Temperature sensor (multi-functional and project-aligned)
- **Eliminated**: Voltage regulators and hand-soldered components (due to reliability issues)

From these lessons, the concept evolved into a **sensor-actuator-controlled AC system**:
- Used **MQTT** to monitor and transmit sensor + motor status
- Created an **app interface** for remote control + real-time feedback
- Developed a system where temperature triggers chilled water flow via a controlled actuator
- While not implementing real chilled water, logic mimics real-world HVAC functionality

---

## Video Presentation

📽️ [Watch Project Video on YouTube](https://www.youtube.com/embed/7UG-YCw4WZ8?si=zjqBop_FBaR4tDm3)

```html
<iframe class="responsive" width="560" height="315" src="https://www.youtube.com/embed/7UG-YCw4WZ8?si=zjqBop_FBaR4tDm3" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
