# 📦 MLOPS — DVC
DVC (Data Version Control) is basically Git for your datasets and machine learning models.
When you work on ML projects, Git can version control your code, but not your large data files or trained models (because they’re too big and change often).

## 1️⃣ Git and DVC Are Separate Tools
1. Git 📝 — Stores and versions small text files  like .py, .ipynb, .yaml, etc.
2. DVC 📂 — Stores and versions large binary files like datasets (.csv, .jpg) or ML models (.pkl, .h5).

## 2️⃣ How They Work Together
When you run dvc add data.csv, two things happen:

### ① DVC Creates a .dvc Metadata File
Example: data.csv.dvc

Contains:

The file’s path

A unique hash (ID) for the current content → md5: a1b2c3...

File size and metadata

DVC uses this hash to know if the file has changed.

### ② You Commit the .dvc File to Git

Git stores the metadata file, not the actual dataset.

The actual large file is stored in DVC’s cache/remote storage.

### 3️⃣ Versioning Process
Every Git commit stores:

Code files (in Git directly)

Metadata files (.dvc), which contain DVC IDs (hashes) for the corresponding data

If you change data.csv and run dvc add data.csv again:

DVC generates a new hash ID

The .dvc file is updated with the new hash

Git sees the .dvc file has changed → commit it → you can always link back to the right data version

### 4️⃣ How IDs and Versions Connect
DVC ID (hash) 🔑 — Unique for that exact version of the file

Git commit ID 🗂 — Captures both:

Code at that time

Metadata pointing to the correct DVC data version

Later, when you check out an old Git commit and run dvc pull:

Git gives you the old .dvc file (with its old hash)

DVC uses that hash to pull the exact matching dataset/model from remote storage

## 💡 Analogy
- Git commit ID = “📸 Snapshot of your whole project”

- DVC hash ID = “🆔 Fingerprint of a specific big file in that snapshot”

- Together: You can go to any old Git commit and still get exactly the same data & model from that time

