# lab.ekamekas.dev

lab.ekamekas.dev is a mono-repository designed as an engineering playground and experimental laboratory.
The core idea of this repository is to solve specific product problems (such as URL Shorteners, Auth Services, Rate Limiters, etc.) and explore them across various tech stacks, architectural patterns, and database implementations.

## 📂 Repository Structure
The repository is organized by domains under the products/ directory. Each project contains a dedicated design specification along with multiple tech stack implementations:
lab.ekamekas.dev/
├── README.md
├── products/
│   ├── url-shortener/                 <-- Example Project Domain
│   │   ├── README.md
│   │   ├── LICENSE
│   │   ├── _design/                   <-- Single source of truth
│   │   │   ├── product_brief.md       <-- Summary of scope, goal, and vision of a product
│   │   │   ├── api.yaml               <-- OpenAPI specification
│   │   │   └── erd.puml               <-- ERD diagram
│   │   │   └── diagrams/
    │   │      └── c4-context.puml     <-- C4 - System Context diagram
    │   │      └── c4-container.puml   <-- C4 - Container diagram
    │   │      └── c4-component.puml   <-- C4 - Component diagram
    │   │      └── seq-flow-a.puml     <-- Sequence of flow A diagram, may has multiple sequence diagram
│   │   │
│   │   └── implementations/           <-- Stack implementations matching the design spec
│   │       ├── node-express-redis/    <-- Node.js + Express + Redis implementation
│   │       ├── go-fiber-postgres/     <-- Go + Fiber + PostgreSQL implementation
│   │       ├── rust-axum-sqlite/      <-- Rust + Axum + SQLite implementation
│   │       └── nextjs-bun-sqlite/     <-- Next.js + Bun + SQLite implementation
│   │
│   └── <other-projects>/              <-- Additional domain experiments
│
└── shared/                            <-- Shared scripts, Docker setups, and configs
    ├── docker/
    └── scripts/


## 📜 Licensing Policy
Because this repository hosts diverse experiments—ranging from open specifications to individual implementations using different open-source packages—licenses may vary by directory. Please refer to the table below for folder-specific licensing rules:


Note: If a specific subfolder inside implementations/ contains its own LICENSE file, the terms in that file override the global matrix above.

## ✨ Contributing & Experiments Guidelines
Design First: Before adding a new stack implementation, ensure the _design/ folder of that project domain has a complete product_brief.md, api.yaml, erd.puml, c4-context.puml, c4-container.puml, c4-component.puml
Consistent Spec: All implementations under implementations/ within the same domain must fulfill the exact contract defined in _design/.
Folder Naming Convention: Name implementation folders using the <language/runtime>-<framework>-<database> format (e.g., go-fiber-postgres).

