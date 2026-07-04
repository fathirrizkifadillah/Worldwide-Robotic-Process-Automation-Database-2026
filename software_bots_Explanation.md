# Software Bots Dataset Explanation (`software_bots.csv`)

## Dataset Overview

### English
This dataset contains 200,000 individual records of deployed software robots (*bots*). It lists session execution metrics like daily tasks processed, execution speed, error rates, and key bot architecture flags (unattended vs. attended, cloud-hosted, AI-assisted, and machine-learning enabled) across various regions.

### Bahasa Indonesia
Dataset ini berisi 200.000 data individu tentang robot perangkat lunak (*bots*) yang dideploy. Dataset ini mencantumkan metrik eksekusi sesi seperti tugas harian yang diproses, kecepatan eksekusi, tingkat kesalahan (*error rate*), dan indikator arsitektur bot utama (unattended vs. attended, cloud-hosted, didukung AI, dan berkemampuan machine-learning) di berbagai wilayah.

## Dataset Structure
- Rows: 200,000
- Columns: 16
- Granularity: Bot-level operational profiles
- Main categorical features: `bot_category`, `bot_status`, `ai_assisted`, `machine_learning_enabled`, `unattended_bot`, `attended_bot`, `cloud_hosted`, `operating_region`
- Target label for prediction: `bot_status` (classification) or `error_rate_percent` (regression)
- Key metrics: `tasks_per_day`, `average_execution_time_seconds`, `error_rate_percent`, `success_rate_percent`

## Column Explanation

| Column | Data Type | English Explanation | Penjelasan Bahasa Indonesia | Analysis Notes |
| --- | --- | --- | --- | --- |
| `bot_id` | String | Unique identifier of the software robot. | ID unik robot perangkat lunak. | Primary Key. Format 'BOT0000001'. |
| `project_id` | String | ID of the project the bot is deployed in. | ID proyek tempat bot dideploy. | Foreign Key linking to `automation_projects.csv`. |
| `bot_name` | String | Unique name assigned to the bot. | Nama unik yang diberikan kepada bot. | Usually contains suffix numbering (e.g. SyncBot-4428). |
| `bot_category` | String | Functional category of the bot. | Kategori fungsional bot. | 40 unique categories (e.g. Meter Reading Bot, Backup Bot). |
| `deployment_date` | Date/String | The date when the bot was deployed. | Tanggal ketika bot dideploy. | Used to measure bot age and seasonality of deployments. |
| `bot_status` | String | Current status of the bot. | Status bot saat ini. | Four unique values: `Idle`, `Maintenance`, `Running`, `Deprecated`. |
| `tasks_per_day` | Integer | Number of automated tasks processed daily. | Jumlah tugas otomatis yang diproses harian. | High tasks/day represent heavy-duty bots (ranges up to 50,000). |
| `average_execution_time_seconds` | Float | Average execution time to complete one task. | Rata-rata waktu eksekusi untuk satu tugas. | Indicates complexity of the automated task. |
| `error_rate_percent` | Float | Percentage of task failures during execution. | Persentase kegagalan tugas selama eksekusi. | Measures bot performance and instability. Ranges up to 40%. |
| `success_rate_percent` | Float | Percentage of successful task completions. | Persentase penyelesaian tugas yang sukses. | Derived directly as `100 - error_rate_percent`. Redundant for ML. |
| `ai_assisted` | String | Flag indicating if the bot uses AI assistance (Yes/No). | Indikator apakah bot menggunakan bantuan AI (Yes/No). | Measures intelligent capabilities. |
| `machine_learning_enabled` | String | Flag indicating if ML models are integrated. | Indikator apakah model ML terintegrasi. | ML-enabled bots might handle unstructured data. |
| `unattended_bot` | String | Flag indicating if the bot runs unattended. | Indikator apakah bot berjalan unattended (tanpa intervensi). | Directly opposes `attended_bot` (binary indicator). |
| `attended_bot` | String | Flag indicating if the bot is attended. | Indikator apakah bot bersifat attended (perlu intervensi). | Directly opposes `unattended_bot` (binary indicator). |
| `cloud_hosted` | String | Flag indicating if the bot is cloud-hosted. | Indikator apakah bot di-host di cloud. | Analyzes infrastructure stability. |
| `operating_region` | String | The global region where the bot operates. | Wilayah global tempat bot beroperasi. | 6 unique global regions. |

## Suggested Analysis Questions

### English
1. Do projects with bots that are `machine_learning_enabled` = 'Yes' show higher throughput and lower error rates?
2. How do unattended bots compare to attended bots in terms of `tasks_per_day` and `average_execution_time_seconds`?
3. What bot categories (e.g. *Backup Bot*, *Invoice Processing Bot*) exhibit the highest average `error_rate_percent`?
4. Does a high error rate trigger a bot status change to `Maintenance` or `Deprecated`?

### Bahasa Indonesia
1. Apakah proyek dengan bot berkemampuan `machine_learning_enabled` = 'Yes' menunjukkan throughput yang lebih tinggi dan tingkat kesalahan yang lebih rendah?
2. Bagaimana perbandingan bot unattended dengan bot attended dalam hal jumlah tugas per hari (`tasks_per_day`) dan rata-rata waktu eksekusi (`average_execution_time_seconds`)?
3. Kategori bot mana (misalnya *Backup Bot*, *Invoice Processing Bot*) yang menunjukkan rata-rata `error_rate_percent` tertinggi?
4. Apakah tingkat kesalahan yang tinggi memicu perubahan status bot menjadi `Maintenance` atau `Deprecated`?

## Useful Derived Features

### English
| Derived Feature | Formula / Idea | Purpose |
| --- | --- | --- |
| `bot_efficiency_index` | `tasks_per_day / average_execution_time_seconds` | Measures bot throughput relative to time constraints. Higher values show optimal processing speed. |
| `is_high_error` | `error_rate_percent > threshold` (e.g., 20%) | Binary flag to easily identify malfunctioning bots for alert modeling. |

### Bahasa Indonesia
| Fitur Turunan | Formula / Ide | Tujuan |
| --- | --- | --- |
| `bot_efficiency_index` | `tasks_per_day / average_execution_time_seconds` | Mengukur throughput bot terhadap kendala waktu. Nilai yang lebih tinggi menunjukkan kecepatan pemrosesan yang optimal. |
| `is_high_error` | `error_rate_percent > threshold` (misal 20%) | Indikator biner untuk mengidentifikasi bot yang bermasalah untuk pemodelan sistem peringatan. |

## Important Notes

### English
- **Redundant Metrics:** `success_rate_percent` is exactly `100 - error_rate_percent`. In machine learning or regression modeling, one of these must be dropped to avoid perfect multicollinearity.
- **Relational Mapping:** 44,021 unique projects have bots mapped in this table out of 50,000 total projects. Around 5,979 projects do not have associated software bots, representing projects in planned phases or with bot-less automation structures.

### Bahasa Indonesia
- **Metrik Redundan:** Kolom `success_rate_percent` bernilai persis `100 - error_rate_percent`. Dalam pemodelan machine learning atau analisis regresi, salah satu kolom ini harus dibuang untuk menghindari multikolinieritas sempurna.
- **Pemetaan Relasional:** Terdapat 44.021 proyek unik yang memiliki bot di tabel ini dari total 50.000 proyek. Sekitar 5.979 proyek tidak memiliki bot terkait, yang merepresentasikan proyek dalam fase terencana (*Planned*) atau proyek tanpa deploy bot.
