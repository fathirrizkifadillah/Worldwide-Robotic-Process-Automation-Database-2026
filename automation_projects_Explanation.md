# Automation Projects Dataset Explanation (`automation_projects.csv`)

## Dataset Overview

### English
This dataset contains 50,000 detailed records of Robotic Process Automation (RPA) projects executed across various global organizations. It records key project metadata, timelines, allocated budgets, financial savings, ROI percentages, department deployment, implementation partners, and technological configurations (such as AI enablement and cloud deployment).

### Bahasa Indonesia
Dataset ini berisi 50.000 data terperinci tentang proyek Robotic Process Automation (RPA) yang dijalankan di berbagai organisasi global. Dataset ini mencatat metadata proyek penting, garis waktu, alokasi anggaran, penghematan finansial, persentase ROI, departemen tempat otomasi diterapkan, mitra pelaksana, dan konfigurasi teknologi (seperti integrasi AI dan cloud).

## Dataset Structure
- Rows: 50,000
- Columns: 18
- Granularity: Project-level deployment logs
- Main categorical features: `project_status`, `automation_type`, `department`, `implementation_partner`, `country`, `industry`
- Target label for prediction: `roi_percent` (regression) or `project_status` (classification)
- Key metrics: `budget_usd`, `annual_savings_usd`, `roi_percent`, `robots_deployed`, `employee_hours_saved`

## Column Explanation

| Column | Data Type | English Explanation | Penjelasan Bahasa Indonesia | Analysis Notes |
| --- | --- | --- | --- | --- |
| `project_id` | String | Unique identifier of the automation project. | ID unik untuk proyek otomasi. | Primary Key. Format like 'PRJ000001'. |
| `company_id` | String | Unique identifier of the company executing the project. | ID unik perusahaan yang mengeksekusi proyek. | Foreign Key linking to `rpa_companies.csv`. |
| `project_name` | String | Name of the automation project. | Nama proyek otomasi. | Standard naming format, often ends with Initiative, Platform, etc. |
| `start_date` | Date/String | The date when the project was started. | Tanggal dimulainya proyek. | Can be parsed as datetime for time-series trend analysis. |
| `completion_date` | Date/String | The date when the project was completed (NaN if Active). | Tanggal selesainya proyek (NaN jika Active). | Contains missing values for active projects (approx. 29.87% of data). |
| `project_status` | String | Current status of the project. | Status proyek saat ini. | Three unique values: `Active`, `Completed`, `Planned`. |
| `automation_type` | String | The functional process being automated. | Jenis proses fungsional yang diotomatisasi. | 25 unique types (e.g., Customer Onboarding, IT Helpdesk). |
| `robots_deployed` | Integer | Number of software robots deployed in the project. | Jumlah robot software yang dideploy dalam proyek. | Ranges from 1 to 50. Key driver of project scale and cost. |
| `budget_usd` | Integer | Total budget allocated to the project in USD. | Total anggaran proyek dalam USD. | Ranges from $10k to $9.5M. |
| `annual_savings_usd` | Integer | Estimated annual financial savings in USD. | Estimasi penghematan finansial tahunan dalam USD. | Used for cost-benefit evaluations. |
| `roi_percent` | Float | Return on Investment percentage. | Persentase ROI (Return on Investment). | Ranges from 15% to 500%. Target variable for value prediction. |
| `department` | String | The business department where automation is implemented. | Departemen bisnis tempat otomasi diterapkan. | 30 unique departments (e.g., Finance, Human Resources). |
| `implementation_partner` | String | External consulting partner who implemented the project. | Mitra konsultasi eksternal yang menerapkan proyek. | 38 unique consulting partners (e.g., Accenture, Capgemini). |
| `country` | String | Country where the project is implemented. | Negara tempat proyek diimplementasikan. | 56 unique countries. |
| `industry` | String | The industry sector of the project. | Sektor industri dari proyek tersebut. | 26 unique industries (e.g., Banking, Healthcare). |
| `employee_hours_saved` | Integer | Total employee hours saved per year. | Total jam kerja karyawan yang dihemat per tahun. | High values indicate successful workflow automation. |
| `ai_enabled` | String | Flag indicating if AI was integrated (Yes/No). | Indikator apakah AI diintegrasikan dalam proyek (Yes/No). | Compare AI vs non-AI project efficiency. |
| `cloud_deployment` | String | Flag indicating cloud deployment (Yes/No). | Indikator apakah proyek dideploy di cloud (Yes/No). | Useful to compare cloud-hosted vs. on-premises projects. |

## Suggested Analysis Questions

### English
1. Which industries achieve the highest ROI, and is there a correlation between project budget and annual savings?
2. What is the ratio of cloud deployment in projects compared to on-premise, and does it differ by global region?
3. Which consulting partner has deployed the highest number of projects and achieved the maximum savings for their clients?
4. Do projects with `ai_enabled` = 'Yes' have higher ROI or more employee hours saved than projects with 'No'?

### Bahasa Indonesia
1. Industri mana yang mencapai ROI tertinggi, dan apakah terdapat korelasi antara anggaran proyek dengan penghematan tahunan?
2. Bagaimana rasio deployment cloud pada proyek dibandingkan dengan on-premise, dan apakah polanya berbeda di setiap wilayah global?
3. Mitra konsultasi mana yang telah mendeploy proyek terbanyak dan menghasilkan penghematan maksimal bagi klien mereka?
4. Apakah proyek dengan `ai_enabled` = 'Yes' memiliki ROI atau penghematan jam kerja karyawan yang lebih tinggi daripada proyek 'No'?

## Useful Derived Features

### English
| Derived Feature | Formula / Idea | Purpose |
| --- | --- | --- |
| `savings_to_budget_ratio` | `annual_savings_usd / budget_usd` | Measures capital efficiency. A ratio > 1 means the project pays for itself in less than a year. |
| `cost_per_robot` | `budget_usd / robots_deployed` | Measures the average development and licensing budget allocated per robot. |

### Bahasa Indonesia
| Fitur Turunan | Formula / Ide | Tujuan |
| --- | --- | --- |
| `savings_to_budget_ratio` | `annual_savings_usd / budget_usd` | Mengukur efisiensi modal. Rasio > 1 berarti proyek mengembalikan modalnya dalam waktu kurang dari satu tahun. |
| `cost_per_robot` | `budget_usd / robots_deployed` | Mengukur anggaran pengembangan dan lisensi rata-rata yang dialokasikan per satu robot. |

## Important Notes

### English
- **Completion Date Nulls:** The missing values in `completion_date` are not anomalies. They are strictly associated with projects under `Active` status, representing active ongoing operations.
- **Representativeness:** As a synthetic database, category distributions and distributions of numeric variables are highly balanced. Patterns represent theoretical scenarios for exploratory analysis and model training, not real production systems.

### Bahasa Indonesia
- **Null pada Tanggal Selesai:** Nilai kosong pada kolom `completion_date` bukan merupakan kejanggalan data. Nilai tersebut mutlak berasosiasi dengan proyek berstatus `Active`, yang mencerminkan operasional proyek yang masih berjalan.
- **Karakter Data Sintetis:** Karena ini adalah database sintetis, distribusi kategori dan variabel numerik sangat seimbang. Pola-pola di dalamnya mewakili skenario teoretis untuk EDA dan pelatihan model, bukan representasi langsung dari sistem produksi nyata.
