# Project Requirements Analysis
**Bioinformatics Projects - Comprehensive Dependency Check**

---

## Summary Status
- ✅ **Python 2.7.18** - Installed
- ✅ **NumPy 1.16.6** - Installed (used by Molecular Dynamics & others)
- ✅ **SciPy 1.2.3** - Installed (required by bio_motif_ensembl)
- ✅ **BioPython 1.76** - Installed (Python 2.7 compatible version; used in several projects)
- ✅ **PyMySQL 0.10.1** - Installed (MySQL-connector alternative)
- ❌ **MySQL-python** - Installation attempted but failed due to Microsoft Visual C++ 9.0 requirement.  (PyMySQL is already in use; you can ignore this or install the VC++ build tools to compile.)
- ✅ **Snakemake** - Installed in Python 3 user environment (`python -m pip install snakemake --user`).
  - Note: `snakemake.exe` lives under `%APPDATA%\Python\Python313\Scripts` which may need to be added to `PATH`.
- ❌ **External Tools** - NOT installed (MEME, AlignACE, MUSCLE, etc.)
- ❌ **Databases** - NOT configured (Ensembl, JASPAR access)

---

## 1. MOLECULAR DYNAMICS PROJECT
**Directory:** `Molecular_Dynamics/`

### Language & Python
- ✅ Python 2.7.18 (installed)

### Python Libraries Required
- ✅ **NumPy 1.16.6** - Installed (numerical computing)
  - Used by: `metropolis_hastings.py`, `replica_exchange.py`, `simulated_annealing.py`
  - Installed via: `C:\Python27\Scripts\pip.exe install numpy`

### External Tools
- None required (pure Python implementation)

### Status
🟢 **Can run** - All dependencies satisfied

---

## 2. BIO_MOTIF_ENSEMBL PROJECT
**Directory:** `bio_motif_ensembl/`

### Language & Python
- ✅ Python 2.7.18 (installed)

### Python Libraries Required
- ✅ **BioPython** - Installed (sequence analysis library)
  - Used by: All files
  - Installed via: `C:\Python27\Scripts\pip.exe install biopython`

- ✅ **SciPy** - Installed (statistical functions)
  - Used by: `Stats.py`
  - Installed via: `C:\Python27\Scripts\pip.exe install scipy`

- ❌ **MySQLdb** - Not installed (MySQL connector)
  - Used by: `Ensembl.py` (Ensembl database queries)
  - Install: `pip install MySQLdb` or `MySQL-python` (PyMySQL may serve as alternative)

### External Tools Required
- ❌ **MEME 4.8.1** - Not installed (motif discovery)
  - Download from: http://meme-suite.org
  - Expected path: `./meme_4.8.1/scripts/meme`

- ❌ **AlignACE** - Not installed (motif finding)
  - Download from: http://www.rsat.eu/
  - Expected path: `./alignace2004/AlignACE`

- ❌ **MUSCLE 3.8.31** - Not installed (sequence alignment)
  - Download from: http://www.drive5.com/muscle/
  - Expected path: `./muscle3.8.31_i86linux64`

### Database Access Required
- ❌ **Ensembl MySQL Server** - Not configured
  - Host: `ensembldb.ensembl.org`
  - User: `anonymous`
  - Requires internet connection and database permissions

- ❌ **JASPAR Database** - Requires internet/API access
  - Used by: `main.py` line 189+
  - URL: `http://jaspar.genereg.net/`

### Status
🔴 **Cannot run** - Missing: BioPython, SciPy, MySQLdb, MEME, AlignACE, MUSCLE, Database access

---

## 3. GENOME ASSEMBLY PROJECT
**Directory:** `genome_assembly/`

### Language & Python
- ✅ Python 2.7.18 (installed)

### Python Libraries Required
- **None** (uses only standard library)

### External Tools
- None required

### Status
🟢 **Can run** - All dependencies available!

---

## 4. COMPARATIVE GENOMICS PROJECT
**Directory:** `comparative_genomics/`

### Language & Python
- ✅ Python 2.7.18 (installed)

### Python Libraries Required
- **None** (uses only standard library)
  - `felsenstein.py` - Pure Python math
  - `nni.py` - Pure Python tree algorithms

### External Tools
- None required

### Status
🟢 **Can run** - All dependencies available!

---

## 5. CRYSTALLOGRAPHY PROJECT
**Directory:** `crystallography/`

### Language & Python
- ✅ Python 2.7.18 (installed)

### Python Libraries Required
- **None** (uses only standard library - optparse, sys)

### External Tools
- None required

### Status
🟢 **Can run** - All dependencies available! ✅ (Already tested and working)

---

## 6. mRNA_MARKUP PROJECT
**Directory:** `mRNA_Markup/`

### Format
- Galaxy Workflow (.ga file)
- XML tool definitions (not standalone Python)

### Requirements
- ❌ **Galaxy Server** - Not installed
- ❌ **ncbi-blast+** - Not installed
- ❌ **BioPython** - Not installed
- ❌ **MuSeqBox** - Not installed

### Status
🔴 **Cannot run** - Requires Galaxy installation and multiple external tools

---

## 7. ROSALIND PROBLEMS
**Directory:** `Rosalind-Problems/`

### Files & Languages
- Python files (.py): **No external dependencies** ✅
- R file (grph.R): Requires R installation
- Java file (fib.java): Requires Java compiler

### Python Requirements
- **None** (uses only standard library)
  - `frmt.py`, `GBK.py`, `gc.py`, etc. - Pure Python with BioPython (but optional)

### Status
🟢 **Python scripts can run** - But BioPython optional for some
🔴 **R/Java scripts need compilers**

---

## 8. SNAKEMAKE PROJECT
**Directory:** `snakemake/`

### Language & Tools
- ✅ **Snakemake** - Installed (Python 3, user site). Use `snakemake` from PATH or via `python -m snakemake`.
  - Used for: Workflow automation in this directory

### Status
🟢 **Can run** - Snakemake available (add to PATH if necessary)

---

## INSTALLATION PRIORITY

### **TIER 1: Easy Setup (Do First)**
The following Python 2.7 packages have been installed already:
```powershell
C:\Python27\Scripts\pip.exe install numpy scipy biopython
``` 
*MySQL-python* remains uninstalled due to build requirements (PyMySQL is used instead).
Snakemake must be installed in a Python 3 environment (see Tier 3 notes below).

### **TIER 2: External Tools (Manual Download)**
1. **MEME Suite** - Download from http://meme-suite.org
2. **MUSCLE** - Download from http://www.drive5.com/muscle/
3. **AlignACE** - Download from http://www.rsat.eu/

### **TIER 3: Database Setup (Complex)**
1. **Ensembl MySQL** - Requires network access to public server
2. **JASPAR** - Requires internet connection to API
3. **Galaxy** - Full installation if mRNA_Markup needed

---

## RUNNABLE PROJECTS NOW

| Project | Status | Why |
|---------|--------|-----|
| Crystallography | ✅ Ready | Only stdlib |
| Genome Assembly | ✅ Ready | Only stdlib |
| Comparative Genomics | ✅ Ready | Only stdlib |
| Rosalind (Python) | ✅ Ready | Stdlib + BioPython available |
| Molecular Dynamics | ✅ Ready | NumPy & SciPy installed ✅ |
| Bio Motif Ensembl | ⚠️ Partial | Python libs ok; external tools & DB needed |
| mRNA_Markup | ❌ Need Galaxy | System-level tool required |
| Snakemake | ✅ Ready | Installed in Python 3 user environment (add to PATH if necessary) |

---

## NEXT STEPS

1. **Install or verify Python packages:** most have been handled above.  If you still need `MySQL-python` you must install the appropriate Visual C++ build tools or continue using `PyMySQL`.

2. **External command‑line tools** (not pip-installable) for `bio_motif_ensembl`:
   * MEME Suite, MUSCLE, AlignACE – download from their respective sites and place executables in the expected subdirectories or on `PATH`.

3. **WSL / Galaxy-specific dependencies** – run the following inside the Ubuntu shell:
   ```bash
   sudo apt update && sudo apt upgrade -y
   sudo apt install -y ncbi-blast+ python3-venv python3-dev build-essential git wget curl libmysqlclient-dev
   cd /mnt/c/Users/91829/bioinformatics-projects
   git clone https://github.com/galaxyproject/galaxy.git    # may take several minutes
   cd galaxy
   python3 -m venv galaxy_env
   source galaxy_env/bin/activate
   pip install -r requirements.txt
   ```
   (the long clone/install steps may be easier to run interactively; the earlier attempt from the assistant timed out.)

4. **Test each project** after installation.

5. **Configure databases** (if Ensembl or JASPAR queries are needed).

---

**Last Updated:** March 2, 2026
