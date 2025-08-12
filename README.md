# CVRRY – Curriculum Format Specification

## 1. Purpose

The **CVRRY** format defines a BibTeX-inspired textual structure for storing and organizing curriculum vitae information in a single file, enabling:

- Grouping data by **entry type**.  
- Supporting multiple **languages** in the same file.  
- Selecting relevant content for different **resume groups**.  
- Prioritizing information display.  
- Ensuring the file is **valid** and processable by automated tools.

---

## 2. General Structure

Each entry follows the syntax:

```bibtex
@<type>{<id>,
    field1 = "value",
    field2 = "value",
    ...
}
````

* **`<type>`**: category of the entry (e.g., `personal`, `experience`, `education`).
* **`<id>`**: unique identifier for the entry within the file (no spaces).
* **`field = "value"`**: key-value pairs with textual information or simple lists.

---

## 3. Reserved Fields

These fields can appear in **any type of entry**:

| Field      | Type    | Required? | Description                                                                                       |
| ---------- | ------- | --------- | ------------------------------------------------------------------------------------------------- |
| `group`    | list    | no        | List of groups the entry belongs to. Separate with commas.                                        |
| `priority` | integer | no        | Importance weight for sorting when no chronological order applies. Lower value = higher priority. |
| `lang`     | string  | no        | Entry language, using ISO code (e.g., `"en"`, `"fr"`, `"pt"`).                                    |
| `note`     | string  | no        | Internal notes not displayed in the final resume.                                                 |

---

## 4. Entry Types and Specific Fields

### 4.1. @personal

Personal information of the candidate.
**Required**: at least **one** `@personal` entry is mandatory for the file to be valid.

Fields:

* `name` (string, required) – Full name.
* `email` (string, optional).
* `phone` (string, optional).
* `address` (string, optional).
* `website` (string, optional).
* `linkedin` (string, optional).
* `github` (string, optional).
* `summary` (string, optional) – Brief professional summary or career objective.

---

### 4.2. @experience

Professional experience history.

Fields:

* `title` (string, required) – Job title or role.
* `company` (string, required).
* `location` (string, optional).
* `start` (string, required, format `YYYY-MM` or `YYYY`).
* `end` (string, optional, `"present"` for ongoing roles).
* `description` (string, optional) – Summary of responsibilities/achievements.

---

### 4.3. @education

Academic education.

Fields:

* `degree` (string, required).
* `institution` (string, required).
* `location` (string, optional).
* `start` (string, required).
* `end` (string, optional).
* `description` (string, optional).

---

### 4.4. @skill

Technical or soft skills.

Fields:

* `skill` (string, required).
* `level` (string, optional) – E.g., "Beginner", "Intermediate", "Advanced".
* `category` (string, optional) – E.g., "Programming", "Leadership".

---

### 4.5. @language

Languages spoken by the candidate.

Fields:

* `language` (string, required) – Name of the language.
* `level` (string, required) – E.g., "Basic", "Fluent".
* `certificate` (string, optional).

---

### 4.6. @certificate

Relevant certifications or courses.

Fields:

* `name` (string, required).
* `institution` (string, optional).
* `year` (string, optional).

---

### 4.7. @project

Relevant projects.

Fields:

* `name` (string, required).
* `description` (string, optional).
* `link` (string, optional).
* `year` (string, optional).

---

### 4.8. @hobby

Hobbies and extracurricular activities.

Fields:

* `name` (string, required).
* `description` (string, optional).

---

## 5. Validity Rules

A CVRRY file is considered **valid** if:

1. It contains **at least one** `@personal` entry.
2. Each entry has a **unique id**.
3. All required fields for each type are present.
4. `start` and `end` fields, when used, follow accepted formats (`YYYY-MM`, `YYYY`, `"present"`).
5. No entry is empty (at least one meaningful field besides reserved ones must be present).

The standard format of a CVRRY file has the extension **.cv**, although any text file that follows the validity standards allows interpretation.

---

## 6. Example of a Valid File

```bibtex
@personal{main,
    name = "Alice Thompson",
    email = "alice.thompson@example.com",
    phone = "+1 555 123 4567",
    summary = "Fullstack developer with 8 years of experience in web and mobile applications.",
    lang = "en",
    group = "dev, us",
    priority = "1"
}

@experience{exp_acme_en,
    title = "Senior Software Engineer",
    company = "Acme Corp",
    location = "New York, USA",
    start = "2018-04",
    end = "present",
    description = "Led the migration of legacy systems to cloud infrastructure, improving scalability and performance.",
    lang = "en",
    group = "dev, us",
    priority = "1"
}

@experience{exp_acme_fr,
    title = "Ingénieure Logiciel Senior",
    company = "Acme Corp",
    location = "New York, USA",
    start = "2018-04",
    end = "present",
    description = "Dirigé la migration des systèmes hérités vers l'infrastructure cloud, améliorant la scalabilité et les performances.",
    lang = "fr",
    group = "dev, france",
    priority = "1"
}

@skill{python_prog,
    skill = "Python",
    level = "Advanced",
    lang = "en",
    group = "dev",
    priority = "1"
}
```

---

**Version:** 1.0  
**Date:** August 12, 2025  
**Status:** Official Draft
