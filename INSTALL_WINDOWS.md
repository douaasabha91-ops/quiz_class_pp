# Windows Installation Guide

This guide provides multiple methods to install the project dependencies on Windows.

## Prerequisites

- Python 3.9 or higher (Python 3.14 may have compatibility issues with some packages)
- PostgreSQL 12 or higher
- Git (optional)

## Method 1: Using Pre-built Wheels (Recommended for Windows)

### Step 1: Upgrade pip

```bash
python -m pip install --upgrade pip setuptools wheel
```

### Step 2: Install packages one by one

This method avoids build issues by installing packages individually:

```bash
pip install streamlit
pip install python-dotenv
pip install pandas
pip install plotly
```

### Step 3: Install PostgreSQL driver (Choose ONE option)

#### Option A: Try psycopg2-binary (pre-built)
```bash
pip install psycopg2-binary
```

If this fails with build errors, try Option B:

#### Option B: Use psycopg3 (better Windows support)
```bash
pip install "psycopg[binary]"
```

If you use Option B, you need to rename the database file:
```bash
# In your project directory
copy database_psycopg3.py database.py
```

## Method 2: Using Anaconda/Miniconda (Easiest)

If you have build issues, using Anaconda is the easiest solution:

### Step 1: Install Miniconda
Download from: https://docs.conda.io/en/latest/miniconda.html

### Step 2: Create environment
```bash
conda create -n quiz_system python=3.11
conda activate quiz_system
```

### Step 3: Install packages
```bash
conda install -c conda-forge streamlit pandas plotly python-dotenv psycopg2
```

## Method 3: Using Python 3.11 (Most Compatible)

If you're using Python 3.14 and facing issues, downgrade to Python 3.11:

### Step 1: Download Python 3.11
- Visit: https://www.python.org/downloads/
- Download Python 3.11.x (latest 3.11 version)

### Step 2: Create virtual environment
```bash
py -3.11 -m venv venv
venv\Scripts\activate
```

### Step 3: Install dependencies
```bash
pip install -r requirements.txt
```

## Common Issues and Solutions

### Issue 1: "Microsoft Visual C++ 14.0 is required"

**Solution:** Install Microsoft C++ Build Tools
1. Download from: https://visualstudio.microsoft.com/visual-cpp-build-tools/
2. Run installer
3. Select "Desktop development with C++"
4. Install

### Issue 2: psycopg2-binary build fails

**Solution 1:** Use psycopg3 instead
```bash
pip install "psycopg[binary]"
# Then rename database_psycopg3.py to database.py
```

**Solution 2:** Use conda
```bash
conda install -c conda-forge psycopg2
```

### Issue 3: Pillow build fails

**Solution:** Install pre-built wheel
```bash
pip install --upgrade Pillow
```

Or use conda:
```bash
conda install pillow
```

### Issue 4: "No module named 'psycopg2'"

If you installed psycopg3, update the imports:
1. Rename `database_psycopg3.py` to `database.py`
2. The app will work with psycopg3

## Verifying Installation

After installation, verify all packages:

```bash
python -c "import streamlit; print('Streamlit OK')"
python -c "import pandas; print('Pandas OK')"
python -c "import plotly; print('Plotly OK')"
python -c "import psycopg2; print('psycopg2 OK')"
# OR if using psycopg3:
python -c "import psycopg; print('psycopg3 OK')"
```

## Next Steps

Once installation is complete:

1. Set up PostgreSQL database (see README.md)
2. Configure .env file
3. Run the application:
   ```bash
   streamlit run app.py
   ```

## Getting Help

If you continue to have issues:

1. Check your Python version: `python --version`
2. Check pip version: `pip --version`
3. Try using a virtual environment
4. Consider using Anaconda (most reliable for Windows)

## Recommended Setup for Students

**For easiest setup:**
1. Install Miniconda
2. Use Method 2 (Anaconda) above
3. This avoids all build tool requirements
