# Galaxy Installation Steps for Your System

## ✅ What You Already Have

- ✅ **WSL 2** (version 2.5.10.0) - Windows Subsystem for Linux
- ✅ **Git** (version 2.53.0)
- ✅ **Python 2.7.18** (Windows)
- ✅ **Python 3.13.1** (Windows)
- ❌ **Ubuntu Linux distribution** - Need to install
- ❌ **Docker** - Optional (can be installed later)

---

## Step 1: Install Ubuntu on WSL2 (2-3 minutes)

### Command
```powershell
# Run in PowerShell as Administrator
wsl --install --distribution Ubuntu-22.04
```

### What to expect:
- Downloads Ubuntu 22.04 LTS (~500MB)
- Installs to: `C:\Users\<username>\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu22.04LTS_79rhkp1fndgsc\`
- Creates new user account
- Completes in 2-3 minutes

### After Installation:
```powershell
# Verify installation
wsl --list --verbose

# Expected output should show Ubuntu-22.04 running on version 2
```

---

## Step 2: Update Ubuntu System Packages

```bash
# Enter WSL Ubuntu terminal
wsl

# Update package manager
sudo apt update && sudo apt upgrade -y

# Install required tools
sudo apt install -y \
  build-essential \
  python3 python3-pip python3-venv \
  git \
  postgresql postgresql-contrib \
  postgresql-client \
  nodejs npm \
  curl wget
```

**Time:** ~5 minutes (depends on internet speed)

---

## Step 3: Clone Galaxy Repository

```bash
# Navigate to your bioinformatics projects
cd /mnt/c/Users/91829/bioinformatics-projects

# Clone Galaxy
git clone https://github.com/galaxyproject/galaxy.git
cd galaxy

# Checkout latest stable release
git checkout release_24.0
```

**Size:** ~150MB download

---

## Step 4: Create Python 3 Virtual Environment

```bash
# Create venv
python3 -m venv galaxy_env

# Activate it
source galaxy_env/bin/activate

# Update pip
pip install --upgrade pip setuptools wheel
```

---

## Step 5: Install Galaxy Dependencies

```bash
# First, ensure you're in the galaxy directory with venv active
cd ~/bioinformatics-projects/galaxy
source galaxy_env/bin/activate

# Install Galaxy
pip install -r requirements.txt

# This takes 5-10 minutes
# Downloads 200+ Python packages
```

---

## Step 6: Initialize Galaxy Database

```bash
# Set up SQLite database
python scripts/manage_db.py upgrade

# Or use PostgreSQL (optional, more complex)
```

---

## Step 7: Configure Galaxy (Optional)

```bash
# Copy default configuration
cp config/galaxy.yml.sample config/galaxy.yml

# Edit if needed (optional for basic usage)
# nano config/galaxy.yml
```

---

## Step 8: Start Galaxy Web Server

```bash
# Make sure venv is activated
source galaxy_env/bin/activate

# Start Galaxy
sh run.sh

# Output should show:
# "The Galaxy application will be available at http://localhost:8080"
```

**Wait:** 30-60 seconds for full startup

---

## Step 9: Access Galaxy Web Interface

### From Windows:
1. Open browser
2. Go to: **http://localhost:8080**
3. Create admin account
4. Set email and password

### From Ubuntu Terminal:
```bash
# If you want to check Galaxy is running
curl http://localhost:8080
```

---

## Step 10: Install BLAST+ (for mRNA_Markup workflow)

```bash
# In WSL Ubuntu terminal (separate from Galaxy run.sh)
# Open new WSL window:
wsl

# Install BLAST
sudo apt install -y ncbi-blast+

# Verify
blastn -version
```

---

## QUICK START COMMANDS

```bash
# 1. Install Ubuntu (PowerShell as Admin)
wsl --install --distribution Ubuntu-22.04

# 2. Enter WSL
wsl

# 3. Update system
sudo apt update && sudo apt upgrade -y

# 4. Install tools
sudo apt install -y build-essential python3 python3-pip git postgresql nodejs npm curl wget

# 5. Clone Galaxy
cd /mnt/c/Users/91829/bioinformatics-projects
git clone https://github.com/galaxyproject/galaxy.git
cd galaxy
git checkout release_24.0

# 6. Setup Python venv
python3 -m venv galaxy_env
source galaxy_env/bin/activate
pip install --upgrade pip

# 7. Install Galaxy
pip install -r requirements.txt

# 8. Initialize database
python scripts/manage_db.py upgrade

# 9. Start Galaxy
sh run.sh

# Then open browser to http://localhost:8080
```

---

## Integration with mRNA_Markup

After Galaxy is running:

```bash
# 1. Copy tools to Galaxy
cp -r /mnt/c/Users/91829/bioinformatics-projects/mRNA_Markup/galaxy_dist/tools/* \
  ~/bioinformatics-projects/galaxy/tools/

# 2. Copy workflow
cp /mnt/c/Users/91829/bioinformatics-projects/mRNA_Markup/Galaxy-Workflow-mRNA_Markup.ga \
  ~/workflows/

# 3. In Galaxy web interface:
#    Admin > Manage Tools > Install or reload
#    Import > Select Galaxy-Workflow-mRNA_Markup.ga
```

---

## Troubleshooting

### "wsl command not found"
```powershell
# Enable WSL in Windows Features
Enable-WindowsOptionalFeature -FeatureName Microsoft-Windows-Subsystem-Linux -Online -NoRestart
```

### Port 8080 already in use
```bash
# Change in config/galaxy.yml
nano config/galaxy.yml

# Find and change:
# http_port: 8081  (or any free port)

# Then restart run.sh
```

### PostgreSQL server errors
```bash
# Restart PostgreSQL
sudo service postgresql restart

# Or use SQLite (default, no extra setup needed)
```

### Galaxy takes too long to start
```bash
# Check logs
tail -f paster.log
```

### Memory or disk space issues
```bash
# Check WSL disk usage
wsl.exe --list --file-format=table
ws --manage --set-sparse=true

# Or increase WSL resource allocation:
# Create C:\Users\<username>\.wslconfig with more RAM/CPU
```

---

## Estimated Timeline

| Step | Time | Task |
|------|------|------|
| 1 | 3 min | Install Ubuntu |
| 2 | 5 min | Update packages |
| 3 | 5 min | Clone Galaxy |
| 4 | 1 min | Create venv |
| 5 | 10 min | Install Galaxy deps |
| 6 | 1 min | Init database |
| 7 | 1 min | Configure |
| 8 | 1 min | Start Galaxy |
| **TOTAL** | **~27 min** | Full installation |

---

## What Happens After Installation

✅ Galaxy admin panel at http://localhost:8080
✅ Upload data and import workflows
✅ Configure BLAST databases
✅ Run mRNA_Markup workflow
✅ Export analysis results
✅ Share workflows with others

---

## To Stop Galaxy

```bash
# Press Ctrl+C in the terminal running run.sh
# To restart:
sh run.sh
```

---

## Next Steps

After installation:

1. **Create workflows** - Use Galaxy web UI
2. **Upload sample data** - Prepare test FASTA files
3. **Configure BLAST database** - Point to bacterial/protein DBs
4. **Run mRNA_Markup** - Execute your analysis
5. **Export results** - Download analysis histoires

---

**Created:** March 2, 2026
**For:** Bioinformatics Projects
**Galaxy Version:** 24.0 (Latest Stable)
**Platform:** WSL2 Ubuntu 22.04 on Windows 10/11
