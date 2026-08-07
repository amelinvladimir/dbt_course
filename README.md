

# dbt_course

A comprehensive, hands-on course repository designed to help you master **dbt (data build tool)**. The project provides step-by-step lessons covering environment setup, core dbt concepts, Jinja templating, testing strategies, package management, and orchestration with Apache Airflow.

## 📚 Course Modules
The repository is organized into numbered directories, each representing a specific lesson or concept:
- `02 Установка dbt/` – Environment setup & prerequisites
- `11 Инкрементальная материализация/` – Incremental models (`append`, `merge`, `delete+insert`)
- `12 seed/` – Loading & configuring CSV seeds
- `13 Snapshots/` – SCD tracking with `timestamp` & `check` strategies
- `14 Configuration/` – Model configs, contracts, & metadata
- `15 Analyses/` – Ad-hoc SQL & compilation
- `16-18 Jinja Introduction/` – Templating syntax, loops, filters, & dbt context
- `19-20 Macros/` – Custom macros, cross-database compatibility, & graph operations
- `21-24 dbt packages/` – `dbt_utils`, `codegen`, `dbt_project_evaluator`, & `automate_dv` (Data Vault)
- `26 select models/` – Selectors, state management, & dependency navigation
- `27-29 Testing/` – Singular, Generic, & Unit tests
- `30 Integration with airflow/` – Orchestration using Astronomer Cosmos & Docker

## 🛠️ Installation & Setup
Follow these steps to prepare your local development environment:

### 1. Prerequisites
- **Python** (3.11 or 3.12 recommended)
- **Git**
- **Docker Desktop**
- **DBeaver** (for DB visualization)
- **Visual Studio Code** with:
  - `dbt Power User` extension
  - `Python` extension

### 2. Clone the Repository
```bash
git clone https://github.com/amelinvladimir/dbt_course.git
cd dbt_course
```

### 3. Virtual Environment & dbt Installation
In VS Code, create a Python virtual environment and install dbt:
```bash
# Windows
python -m pip install dbt-postgres

# macOS
python3 -m pip install dbt-postgres
```
Verify installation:
```bash
dbt --version
```

## 🗄️ Database & Profile Configuration

### 1. Start PostgreSQL Container
Run the following Docker command to launch a pre-configured PostgreSQL database:
```bash
docker run --name dbt-course-postgres \
  -e POSTGRES_PASSWORD=mysecretpassword \
  -p 4001:5432 \
  -d amelinvd/dbt_course_postgres_db_multiplatform
```
*(Fallback image: `amelinvd/dbt_course_postgres_db`)*

**DBeaver Connection Details:**
- Host: `localhost` | Port: `4001`
- DB: `postgres` | User: `postgres` | Pass: `mysecretpassword`

### 2. Configure `profiles.yml`
Create `~/.dbt/profiles.yml` and add:
```yaml
dbt_course:
  outputs:
    dev:
      dbname: dbt_course
      host: localhost
      pass: mysecretpassword
      port: 4001
      schema: bookings_dbt
      threads: 4
      type: postgres
      user: postgres
  target: dev
```

## 🚀 Usage & Common Commands
Once configured, you can run dbt commands from the project root or within specific module directories:

| Command | Description |
|---------|-------------|
| `dbt deps` | Install packages defined in `packages.yml` |
| `dbt seed` | Load CSV seeds into the database |
| `dbt run` | Compile & execute SQL models |
| `dbt test` | Run singular & generic tests |
| `dbt build` | Run seeds, models, snapshots & tests in dependency order |
| `dbt compile` | Generate SQL without executing it |
| `dbt run --select model_name` | Target specific models or use selectors |

**Examples from the course:**
```bash
# Run only models tagged with 'bookings'
dbt build --select 'tag:bookings'

# Test a specific model
dbt test -s stg_flights__seats

# Compile an analysis file
dbt compile --select cancelled_fligths_mirniy
```

## 📝 Notes
- This repository is designed for educational purposes and assumes basic SQL knowledge.
- Some modules reference external course links for Docker/SQL setup; follow the provided README files in each directory for detailed steps.
- For Airflow integration (Module 30), ensure Docker Compose is running and network bridges are correctly connected between the Airflow stack and the PostgreSQL container.
- All code examples are tested with `dbt-postgres` and Python 3.11/3.12.
