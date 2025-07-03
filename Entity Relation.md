### 📌 Definition

- **ER Model**: High-level data model used to define the data elements and relationships between them.
    
- Represents **real-world entities** and their **interactions**.
    

---

### 🧱 Components

#### 🟦 Entities

- **Entity**: Object in the real world (e.g., Student, Course).
    
- **Entity Set**: Collection of similar entities.
    
- **Types**:
    
    - **Strong Entity**: Has a primary key.
        
    - **Weak Entity**: Doesn’t have a primary key; depends on a strong entity.
        

#### 🔑 Attributes
- Properties of an entity.
    
- **Types**:
    
    - **Simple (Atomic)**: indivisible (e.g., age)
        
    - **Composite**: can be broken down (e.g., name → first, last)
        
    - **Derived**: can be calculated (e.g., age from DOB)
        
    - **Multivalued**: multiple values (e.g., phone numbers)
        

#### 🔗 Relationships

- **Relationship**: Association among entities (e.g., Student **enrolls** in Course).
    
- **Degree**: Number of entity sets involved (binary, ternary, etc.)
    
- **Cardinality**:
    
    - **1:1**, **1:N**, **M:N**
        
- **Participation**:
    
    - **Total**: Every entity must participate.
        
    - **Partial**: Some may not participate.
        

#### 📐 Keys in ER

- **Primary Key**: Uniquely identifies an entity.
    
- **Discriminator (Partial Key)**: Identifies weak entity relative to strong entity.
    

---

### 🛠️ Diagram Notations

- **Rectangle** → Entity
    
- **Ellipse** → Attribute
    
- **Diamond** → Relationship
    
- **Double Rectangle** → Weak Entity
    
- **Double Ellipse** → Multivalued Attribute
    
- **Underline** → Primary Key
    
- **Dashed Ellipse** → Derived Attribute
    

---
### 🔄 Conversion to Tables

- Strong Entity → Table with all attributes.
    
- Weak Entity → Table with foreign key + discriminator.
    
- Relationship → New table (for many-to-many), or foreign keys (for 1:1 or 1:N).