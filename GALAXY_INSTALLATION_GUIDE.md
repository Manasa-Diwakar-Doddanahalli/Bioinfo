# Galaxy Framework Installation Guide
**Date:** March 2, 2026  
**Target System:** Windows 10/11 with Python 2.7

---

## Important Notice

⚠️ **Galaxy is primarily designed for Linux/Unix systems**. Windows installation is challenging but possible using:

1. **WSL 2 (Windows Subsystem for Linux)** - Recommended ✅
2. **Docker Desktop** - Alternative
3. **VirtualBox/VM** - Full Linux environment
4. **Cygwin** - Limited support

---

## System Requirements

| Requirement | Your System | Status |
|------------|-------------|--------|
| Python 3.6+ | Python 2.7 + 3.13 | ⚠️ Galaxy needs Python 3 |
| Git | ? | Check needed |
| Database (PostgreSQL/SQLite) | Not installed | Install needed |
| Node.js | ? | Check needed |
| 2GB RAM minimum | Unknown | Should have |
| 5GB disk space | Available | ✅ |
| Linux kernel | Windows 10/11 | ⚠️ Need WSL2 |

---

## METHOD 1: WSL 2 (Recommended for Windows)

### Prerequisites
- Windows 10 v2004+ or Windows 11
- Administrator privileges
- 5GB disk space

### Step 1: Enable WSL 2

```powershell
# Run as Administrator
wsl --install

# Or manually enable features
Enable-WindowsOptionalFeature -FeatureName Microsoft-Windows-Subsystem-Linux -Online
Enable-WindowsOptionalFeature -FeatureName VirtualMachinePlatform -Online
```

### Step 2: Install Ubuntu on WSL 2

```powershell
wsl --install -d Ubuntu-22.04
wsl --set-default-version 2
```

### Step 3: Update Ubuntu packages

```bash
# Inside WSL Ubuntu terminal
sudo apt update && sudo apt upgrade -y
sudo apt install python3 python3-pip git postgresql postgresql-contrib -y
```

### Step 4: Download Galaxy

```bash
cd ~
git clone https://github.com/galaxyproject/galaxy.git
cd galaxy
git checkout release_24.0  # Latest stable release
```

### Step 5: Install Galaxy dependencies

```bash
# Python 3 venv
python3 -m venv galaxy_env
source galaxy_env/bin/activate

# Install Galaxy
pip install -r requirements.txt
```

### Step 6: Configure Galaxy

```bash
# Copy default config
cp config/galaxy.yml.sample config/galaxy.yml

# Edit configuration (optional)
# nano config/galaxy.yml
```

### Step 7: Start Galaxy

```bash
# Start database
sudo service postgresql start

# Start Galaxy web server
sh run.sh
```

**Access Galaxy:** http://localhost:8080

---

## METHOD 2: Docker (Easier Alternative)

### Prerequisites
- Docker Desktop installed
- 4GB RAM allocated to Docker
- 10GB disk space

### Installation Steps

```powershell
# Install Docker Desktop (one-time setup)
# Download from: https://www.docker.com/products/docker-desktop

# After Docker is running, create Galaxy container
docker run -d -p 8080:80 bgruening/galaxy-stable:latest

# Wait 1-2 minutes for Galaxy to start
# Access at: http://localhost:8080
```

**Easy commands:**
```powershell
# Check container status
docker ps

# View logs
docker logs <container_id>

# Stop Galaxy
docker stop <container_id>

# Start Galaxy again
docker start <container_id>
```

---

## METHOD 3: Manual Installation on Windows (NOT RECOMMENDED)

### Prerequisites
- Python 3.9+
- Git for Windows
- PostgreSQL
- Node.js

### Steps

1. **Install Python 3**
   ```powershell
   # Install from python.org or via pip
   ```

2. **Install Git**
   ```powershell
   # Download from https://git-scm.com/download/win
   ```

3. **Install PostgreSQL**
   ```powershell
   # Download from https://www.postgresql.org/download/windows/
   ```

4. **Clone Galaxy**
   ```powershell
   git clone https://github.com/galaxyproject/galaxy.git
   cd galaxy
   ```

5. **Create Python environment**
   ```powershell
   python -m venv galaxy_env
   galaxy_env\Scripts\activate
   ```

6. **Install dependencies**
   ```powershell
   pip install -r requirements.txt
   ```

7. **Run Galaxy**
   ```powershell
   python scripts/galaxyapp/galaxy.py
   ```

---

## Compatibility with mRNA_Markup Workflow

### After Galaxy Installation:

```bash
# Copy mRNA_Markup tool files
cp -r ../bioinformatics-projects/mRNA_Markup/galaxy_dist/* galaxy/config/

# Install BLAST
sudo apt install ncbi-blast+ -y

# Install BioPython (if needed)
pip install biopython

# Restart Galaxy
# Navigate to http://localhost:8080
# Import Galaxy-Workflow-mRNA_Markup.ga via web interface
```

---

## QUICK COMPARISON

| Method | Difficulty | Compatibility | Recommended |
|--------|-----------|--------------|-------------|
| WSL 2 | Medium | Excellent | ✅ YES |
| Docker | Easy | Excellent | ✅ YES |
| Manual Windows | Hard | Limited | ❌ NO |

---

## Troubleshooting

### Galaxy won't start
```powershell
# Check logs
docker logs <container_id>
# WSL: journalctl -u galaxyd -f
```

### Port 8080 already in use
```powershell
# Change port in config
# docker: docker run -p 9999:80 ...
# WSL: edit config/galaxy.yml
```

### Database connection errors
```bash
# WSL: Restart PostgreSQL
sudo service postgresql restart
sudo -u postgres psql -c "CREATE DATABASE galaxy;"
```

### Memory/Performance issues
```powershell
# Docker: Increase memory
# Settings > Resources > Memory (4GB+)
```

---

## Next Steps After Installation

1. **Access Galaxy Web UI**
   - URL: http://localhost:8080
   - Create admin account
   - Configure tools

2. **Import mRNA_Markup Workflow**
   - File > Import workflow
   - Select: Galaxy-Workflow-mRNA_Markup.ga

3. **Install Tools**
   - Admin > Manage Tools
   - Install BLAST+, Biopython dependencies

4. **Configure Databases**
   - Add BLAST databases
   - Upload bacterial contamination DB
   - Setup protein reference databases

---

## QUICK INSTALL COMMAND (Docker - Fastest)

```powershell
# Requires Docker Desktop installed
docker run -d \
  --name=galaxy \
  -p 8080:80 \
  -p 8021:21 \
  -v galaxy_storage:/export \
  bgruening/galaxy-stable:latest

# Wait 2 minutes, then open browser
Start-Process "http://localhost:8080"
```

---

## Recommendation for Your System

Since you're on Windows with both Python 2.7 and 3.13:

**BEST OPTION: Docker + Galaxy**
- ✅ Easiest to install
- ✅ No system conflicts
- ✅ Pre-configured environment
- ✅ Works with mRNA_Markup workflow
- ✅ Can be deleted/reinstalled easily

**SECOND OPTION: WSL 2 + Galaxy**
- ✅ Full Linux environment
- ✅ Integrates with Windows
- ⚠️ More complex setup
- ✅ Direct control over configuration

**AVOID: Manual Windows installation**
- ❌ Many compatibility issues
- ❌ Difficult to debug
- ❌ Slow performance

---

**Installation Date:** March 2, 2026
**Galaxy Version:** 24.0 (Latest stable)
**Architecture:** 64-bit Windows
