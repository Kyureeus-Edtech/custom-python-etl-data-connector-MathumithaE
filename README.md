# Spamhaus & NVD ETL Data Connector

This project extracts threat intelligence data from the **Spamhaus DROP** List and the **NVD CVE Feed**, transforms it, and loads it into **MongoDB**. It is designed for ingesting malicious IP networks and vulnerability data for cybersecurity monitoring and analysis.
<u> </u>

##  1. Clone or Download the Project
```
git clone https://github.com/your-username/spamhaus-nvd-etl.git
cd spamhaus-nvd-etl
```


If you don’t have a repository, place your elt.py, .env, and requirements.txt files in the same folder.

## 2. Create and Activate a Virtual Environment

### Windows (CMD or PowerShell):

```
python -m venv venv
venv\Scripts\activate
```


### macOS / Linux:
```
python3 -m venv venv
source venv/bin/activate
```

# 3. Install Dependencies

Install the required Python packages:
```
pip install -r requirements.txt
```


If you don’t yet have requirements.txt, create it with:
```
pymongo==4.10.1
python-dotenv==1.0.1
requests==2.32.3
```

## 4. Create and Configure .env File

The .env file stores private configuration values used by the ETL script. Place it in the root folder of the project (next to elt.py).

Example .env:
```
# MongoDB Configuration

MONGODB_URI=mongodb://localhost:27017/
MONGODB_DB=etl_database
MONGODB_COLLECTION_SPAMHAUS=spamhaus_drop
MONGODB_COLLECTION_CVE=nvd_cve

# Feed URLs
SPAMHAUS_URL=https://www.spamhaus.org/drop/drop.txt
NVD_URL=https://services.nvd.nist.gov/rest/json/cves/2.0
```

Replace these values with your actual connection string and database/collection names.

## 5. Run the ETL Script
```
python elt.py
```

The script will:

Fetch the latest malicious IP ranges from the Spamhaus DROP List

Fetch the latest vulnerability data from the NVD CVE feed

Transform the data into a structured JSON format

Insert the records into the MongoDB collections spamhaus_drop and nvd_cve

## 6. Verify Data in MongoDB

If MongoDB is running locally:

```
mongo
use etl_database
db.spamhaus_drop.find().limit(5).pretty()
db.nvd_cve.find().limit(5).pretty()
```


You should see a sample of inserted IP ranges and CVE records.

## 7. Project Highlights

**Automated ETL** for cybersecurity threat intelligence.

Supports **multiple data sources** (TXT and JSON feeds).

Stores data in **MongoDB** for easy querying and analysis.

Can be extended for **dashboards, alerts, or automated reports**.
