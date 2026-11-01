![[file-20d1f3e9dd8061d0e7bee29a72abbc26.png]]

**Question:** Using the scenario, explain how ontologies enable **semantic interoperability** between different systems. In your answer, refer to at least **two** ontology components (e.g., class, relationship, axiom) to explain how the mapping is achieved. *(5 marks)*

**Scenario:** A patient visits a hospital in Kandy. The doctor records the diagnosis using the hospital's local system as "high sugar". This record is later sent electronically to a specialist in Colombo whose system uses the code "E11 - Type 2 Diabetes Mellitus" (ICD-10 standard). The two systems are integrated using SNOMED CT, a medical ontology, allowing both systems to understand that "high sugar" maps to "Type 2 Diabetes Mellitus."

---

## 1. What semantic interoperability means here

Semantic interoperability means different systems can exchange data **and** interpret it with the same meaning.

In the scenario, the Kandy hospital records the free-text term "high sugar", while the Colombo specialist's system uses the ICD-10 code **E11** (Type 2 Diabetes Mellitus). Without a shared meaning, the Colombo system would not know what "high sugar" refers to. The ontology (SNOMED CT) supplies that shared, machine-readable meaning.

---

## 2. How the ontology achieves the mapping

### a) Classes (concepts)

- SNOMED CT represents each medical idea as a **class** with a unique concept identifier, for example the class *Type 2 Diabetes Mellitus*.
- The Kandy term "high sugar" is recorded as a **synonym** (description) attached to that class.
- The ICD-10 code **E11** is linked to the same class.
- "High sugar" and "E11" therefore point to the **same concept**, even though the wording and codes differ.

### b) Relationships (properties)

- Classes are connected by relationships such as **is-a** (Type 2 Diabetes Mellitus *is-a* Diabetes Mellitus *is-a* Disorder of glucose metabolism) and **finding site / associated finding** (for example, linking the disease to raised blood glucose).
- These links let the systems understand the term **in context**, so "high sugar" is resolved to the right disease class instead of being treated as a plain text string.

### c) Axioms (rules and constraints)

- Axioms are logical statements that formally define a class, for example "Type 2 Diabetes Mellitus is a kind of diabetes mellitus that is not insulin-dependent".
- They allow a reasoner to **infer and check** mappings automatically, such as confirming that the synonym "high sugar" and code E11 refer to the same concept, and they prevent wrong mappings.

---

## 3. The result in the scenario

1. Kandy records "high sugar", which the local system maps to the SNOMED CT class *Type 2 Diabetes Mellitus*.
2. The record is sent electronically with that concept identifier.
3. Colombo's system maps the same SNOMED CT class to ICD-10 code **E11**.
4. The specialist sees the correct diagnosis, with no manual translation and no loss of meaning.

---

## One-line summary

> Ontologies enable semantic interoperability by defining shared **classes, relationships and axioms**, so different terms and code systems ("high sugar" and E11) map to the same concept (Type 2 Diabetes Mellitus) and both systems interpret the data identically.

