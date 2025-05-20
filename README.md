# Consent-Level Digital Use Conditions Schema

This repository provides a JSON Schema for modeling **consent-level Digital Use Conditions (DUC)** — a structured, machine-readable framework for capturing how individual or group consent governs the use of digital assets.

---

## 🎯 Purpose

This schema enables precise documentation of consent-related use conditions that can be directly tied to specific digital assets (e.g., datasets, records, files). It supports:

- **Granular consent tracking** at the asset level
- Modelling of **condition clusters** that describe rules under which data may be used
- Linking of conditions to **specific assets** 
- Capturing **consent decisions**, timestamps, and individual responses

---

## 🔍 Key Features

- **Consent-Centric Design**: Focuses exclusively on conditions driven by user or subject consent
- **Condition Clusters**: Modular condition structures including rule types and terms
- **Explicit Asset Linkage**: Conditions are tied to one or more assets via unique identifiers
- **Flexible Extensions**: Support for additional metadata via termParameter and conditionParameter
- **Strong Validation**: Conforms to [JSON Schema Draft 07](http://json-schema.org/draft-07/schema)

---

## 🧩 Schema Overview

| Field | Description |
|-------|-------------|
| `conditions` | Main array of condition entries, each with associated asset IDs, and consent |
| `ConditionCluster` | Array of rule-driven terms (e.g., Permitted, Forbidden) defining allowed uses |
| `assetsIdList` | List of asset identifiers this condition applies to |
| `consent` | Consent decision (e.g., Given, Refused), with date and narrative response |
| `assets` | Optional asset metadata such as name, description, and external references |
| `profileId`, `ducVersion`, `creationDate`, etc. | Metadata for versioning and traceability |

---

## 📄 Versioning

- **Current Version**: `1.0.1`
- **Schema Draft**: [JSON Schema Draft 2020-12](https://json-schema.org/draft/2020-12/schema)

---

## 📘 Full Example

- **Note**: This is a hypothatical example of a duc profile

```json
{
  "profileId": "https://consent-data.org/duc/consent-001",
  "profileVersion": "1.0.0",
  "profileName": "Rare Disease Consent Profile",
  "ducVersion": "1.0.1",
  "creationDate": "2025-01-10",
  "lastUpdated": "2025-05-12",
  "permissionMode": "All unstated conditions are Forbidden",
  "language": "eng",
  "assets": [
    {
      "assetId": "asset-001",
      "assetName": "Rare Disease Genome Dataset",
      "assetDescription": "Whole genome sequencing data from participants with a rare genetic disorder.",
      "assetReferences": [
        "https://doi.org/10.1000/example-rare-disease"
      ],
      "assetURI": "https://datarepository.org/assets/asset-001"
    }
  ],
  "conditions": [
    {
      "conditionCluster": [
        {
          "term": {
            "label": "Geographical Area",
            "uri": "http://example.org/parameters/GeographicalArea"
          },
          "rule": "Permitted",
          "termParameter": [
            {
              "label":"Europe",
              "uri": "http://example.org/parameters/GeographicalArea/Europe"  
            }
          ]
          
        },
        {
          "term": {
            "label": "Commercial Entity"
          },
          "rule": "Forbidden"
        }
      ],
      "conditionparameter": {
        "label": "Subject to participant consent"
      },
      "assetsIdList": ["asset-001"],
      "consent": {
        "status": "Given",
        "date": "2025-01-01T10:00:00Z",
        "response": "Consent given for disease-specific clinical research within Europe. No commercial use permitted."
      }
    }
  ]
}


