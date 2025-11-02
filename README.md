# Clinical Pathway Markup Language (CPML)

**Version:** 1.0  
**Status:** Public Specification  
**Developed by:**  
Research Institute for Oncology, Hematology and Cell Therapy (RIOHCT)  
Tehran University of Medical Sciences  
© 2025 RIOHCT — All Rights Reserved

---

## Overview

The **Clinical Pathway Markup Language (CPML)** is a standardized XML-based language for defining, executing, and exchanging clinical pathways in oncology, hematology, and cell therapy.

CPML provides a structured framework to model evidence-based workflows such as diagnosis, treatment, and follow-up.  
It transforms complex clinical decision logic into structured, machine-readable and interoperable formats suitable for electronic health systems and research registries.

---

## Purpose

CPML was developed to:

- Standardize clinical pathways across care providers  
- Enable decision support and workflow automation  
- Improve consistency and quality of care  
- Facilitate integration with registries and research databases  
- Provide an open and extensible structure for clinical protocol representation  

---

## Key Features

- **XML-based syntax** — interoperable and human-readable  
- **Workflow nodes** — `start`, `decision`, `process`, `subpathway`, `end`  
- **Variable definitions** — structured data inputs from HIS, LIS, or manual entry  
- **Decision logic** — embedded conditional expressions  
- **Validation & testing** — structural, clinical, and drug-compatibility checks  
- **Inheritance model** — supports parent/child pathways for specialization  
- **Version control & governance** — lifecycle management and institutional approval

---

## Example Snippet

```xml
<cpml id="ALL-RISK-STRAT" version="1.0">
  <metadata>
    <title>ALL Risk Stratification</title>
    <description>Risk grouping for Acute Lymphoblastic Leukemia</description>
  </metadata>

  <variables>
    <var name="blast" type="float" ask="Blast percentage?" required="true" source="LIS"/>
    <var name="age" type="integer" ask="Patient age?" required="true" source="HIS"/>
  </variables>

  <nodes>
    <start id="S1"/>
    <decision id="D1" label="High risk?">
      <condition>[[blast]] >= 30 OR [[age]] > 60</condition>
      <yes goto="P2"/>
      <no goto="P3"/>
    </decision>
    <process id="P2">
      <action>Arm B – High Risk Protocol</action>
    </process>
    <process id="P3">
      <action>Arm A – Standard Risk Protocol</action>
    </process>
    <end id="E1"/>
  </nodes>
</cpml>
