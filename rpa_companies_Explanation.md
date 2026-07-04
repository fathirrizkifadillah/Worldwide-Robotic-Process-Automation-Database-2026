# RPA Companies Dataset Explanation (`rpa_companies.csv`)

## Dataset Overview

### English
This dataset contains profiles of 5,000 organizations that leverage or provide RPA platforms. It includes institutional details such as headquarters location, foundation year, size indicators (employee count, annual revenue), the specific RPA platform adopted (e.g., UiPath, Robocorp), and system capability levels (such as cloud readiness, low-code support, and process mining tools).

### Bahasa Indonesia
Dataset ini berisi profil dari 5.000 organisasi yang menggunakan atau menyediakan platform RPA. Dataset ini mencakup detail institusional seperti lokasi kantor pusat, tahun pendirian, indikator ukuran perusahaan (jumlah karyawan, pendapatan tahunan), platform RPA spesifik yang diadopsi (misalnya UiPath, Robocorp), dan tingkat kapabilitas sistem (seperti kesiapan cloud, dukungan low-code, dan process mining).

## Dataset Structure
- Rows: 5,000
- Columns: 17
- Granularity: Company-level profile records
- Main categorical features: `headquarters_country`, `rpa_platform`, `cloud_support`, `ai_integration`, `global_region`, `industry_focus`
- Target label for prediction: `market_share_percent` or `annual_revenue_usd`
- Key metrics: `annual_revenue_usd`, `employee_count`, `market_share_percent`, `customer_count`

## Column Explanation

| Column | Data Type | English Explanation | Penjelasan Bahasa Indonesia | Analysis Notes |
| --- | --- | --- | --- | --- |
| `company_id` | String | Unique identifier for the company. | ID unik untuk perusahaan. | Primary Key. Format 'CMP00001'. |
| `company_name` | String | Official name of the company. | Nama resmi perusahaan. | 5,000 unique records. |
| `headquarters_country` | String | Country where company HQ is located. | Negara lokasi kantor pusat perusahaan. | 56 unique countries. |
| `headquarters_city` | String | City where company HQ is located. | Kota lokasi kantor pusat perusahaan. | 262 unique cities. |
| `founded_year` | Integer | Year the company was founded. | Tahun pendirian perusahaan. | Ranges from 1985 to 2024. Indicates organizational maturity. |
| `employee_count` | Integer | Total number of employees. | Jumlah total karyawan. | Ranges from 5 to 10,224. |
| `annual_revenue_usd` | Integer | Annual revenue of the company in USD. | Pendapatan tahunan perusahaan dalam USD. | Ranges from $1M to $6.6B. Indicates organizational scale. |
| `rpa_platform` | String | The primary RPA software platform used. | Platform perangkat lunak RPA utama yang digunakan. | 34 unique platforms (e.g., WorkFusion, SAP iRPA, UiPath). |
| `cloud_support` | String | Level of cloud computing support. | Tingkat dukungan komputasi awan. | Three unique values: `Yes`, `Partial`, `No`. |
| `ai_integration` | String | Level of AI integration in their automation. | Tingkat integrasi AI dalam otomasi mereka. | Three unique values: `Yes`, `Partial`, `No`. |
| `process_mining_support` | String | Flag indicating process mining support. | Indikator dukungan penambangan proses. | Binary values: `Yes`, `No`. |
| `low_code_support` | String | Flag indicating low-code development support. | Indikator dukungan pengembangan low-code. | Binary values: `Yes`, `No`. |
| `market_share_percent` | Float | Estimated company market share in the industry. | Estimasi pangsa pasar perusahaan di industri. | Ranges from 0.001% to 2.73%. |
| `customer_count` | Integer | Number of active customers/clients. | Jumlah pelanggan/klien aktif. | Indicates commercial footprint (ranges from 1 to 13,470). |
| `industry_focus` | String | Primary industry sector the company targets. | Sektor industri utama yang difokuskan perusahaan. | 26 unique sectors (e.g., Professional Services). |
| `website` | String | Company's official URL. | URL resmi situs web perusahaan. | Clean website links. |
| `global_region` | String | Global region of the company HQ. | Wilayah global lokasi kantor pusat perusahaan. | 6 unique regions (Europe, Africa, South America, etc.). |

## Suggested Analysis Questions

### English
1. Which RPA platforms (e.g., UiPath, SAP iRPA, Robocorp) are associated with the largest average revenues or the highest customer counts?
2. Do larger companies (higher annual revenue and employee count) deploy projects with larger budgets and more robots?
3. How does cloud computing support and AI integration levels correlate with the target industry focus of these companies?
4. What global regions dominate the RPA market in terms of total customer counts and market share?

### Bahasa Indonesia
1. Platform RPA mana (seperti UiPath, SAP iRPA, Robocorp) yang terasosiasi dengan pendapatan perusahaan rata-rata terbesar atau jumlah pelanggan terbanyak?
2. Apakah perusahaan yang lebih besar (pendapatan tahunan dan jumlah karyawan tinggi) cenderung mendanai proyek dengan anggaran lebih besar dan mengerahkan lebih banyak robot?
3. Bagaimana tingkat dukungan komputasi awan dan tingkat integrasi AI berkorelasi dengan fokus industri target dari perusahaan-perusahaan tersebut?
4. Wilayah global mana yang mendominasi pasar RPA dalam hal jumlah total pelanggan dan pangsa pasar?

## Useful Derived Features

### English
| Derived Feature | Formula / Idea | Purpose |
| --- | --- | --- |
| `revenue_per_employee` | `annual_revenue_usd / employee_count` | Indicates productivity and operational efficiency of the implementing company. |
| `avg_revenue_per_customer` | `annual_revenue_usd / customer_count` | Estimates the average value of each customer for the company. |

### Bahasa Indonesia
| Fitur Turunan | Formula / Ide | Tujuan |
| --- | --- | --- |
| `revenue_per_employee` | `annual_revenue_usd / employee_count` | Mengindikasikan produktivitas dan efisiensi operasional dari perusahaan yang mengimplementasikan. |
| `avg_revenue_per_customer` | `annual_revenue_usd / customer_count` | Mengestimasi nilai rata-rata dari setiap pelanggan bagi perusahaan. |

## Important Notes

### English
- **Relational Integrity:** All company IDs represented in the projects dataset exist here, ensuring there are no projects deployed by unregistered organizations.
- **Size Variance:** The dataset captures a wide variety of organization scales, from small startups with 5 employees to global conglomerates with revenues over $6 Billion.

### Bahasa Indonesia
- **Integritas Relasional:** Semua ID perusahaan yang terdaftar pada dataset proyek ada di tabel ini, memastikan tidak ada proyek otomasi yang dijalankan oleh organisasi tak terdaftar.
- **Variansi Ukuran:** Dataset ini mencakup berbagai macam skala organisasi, dari startup kecil dengan 5 karyawan hingga konglomerat global dengan pendapatan di atas \$6 Miliar.
