# Automated Weather Data Workflow

## Project Overview
The **Automated Weather Data Workflow** is a dynamic and scalable ETL pipeline designed to fetch, process, and store weather data in real time. Built using Apache Airflow, this project integrates with AWS RDS and the Open-Meteo API to automate the extraction, transformation, and loading (ETL) of weather data. This pipeline ensures efficient data processing, seamless database integration, and consistent monitoring.

## Key Features
- **Data Extraction**: Fetches real-time weather data, including temperature, wind speed, wind direction, and weather conditions, from the Open-Meteo API.
- **Data Transformation**: Processes and validates raw API data into a structured format for database storage.
- **Data Loading**: Stores transformed data in a robust AWS RDS PostgreSQL database for further analysis and querying.
- **Scalability**: Configured to run daily but easily extendable to handle different schedules or datasets.
- **Monitoring and Automation**: Leverages Apache Airflow’s robust DAG monitoring and task scheduling features for end-to-end automation.

## Workflow
The ETL pipeline consists of three main tasks:

1. **Extract Weather Data**:
   - Connects to the Open-Meteo API via an HTTP hook.
   - Retrieves weather data for a specific latitude and longitude.

2. **Transform Weather Data**:
   - Processes raw weather data and validates key parameters.
   - Ensures data integrity by handling missing or invalid fields.

3. **Load Weather Data**:
   - Connects to AWS RDS using PostgreSQL.
   - Creates a table (if not already existing) and inserts transformed data.

### DAG Workflow in Airflow
The pipeline’s DAG structure is as follows:
- **extract_weather_data**: Extracts raw weather data.
- **transform_weather_data**: Transforms raw data into a structured format.
- **load_weather_data**: Loads the transformed data into the AWS RDS PostgreSQL database.

## Prerequisites

### Software Requirements
- **Python 3.8+**
- **Apache Airflow 2.5+**
- **Docker** (for containerized execution)
- **AWS RDS PostgreSQL Instance**

### Python Dependencies
Install the required Python libraries using:
```bash
pip install apache-airflow apache-airflow-providers-http apache-airflow-providers-postgres
```

### Environment Setup
1. Configure the following Airflow connections:
   - **`open_meteo_api`**:
     - **Type**: HTTP
     - **Host**: `https://api.open-meteo.com`
   - **`postgres_default`**:
     - **Type**: Postgres
     - **Host**: Your AWS RDS endpoint
     - **Port**: `5432`
     - **Username**: `<username>`
     - **Password**: `<password>`
     - **Database**: `<dbname>`

2. Set up AWS RDS PostgreSQL:
   - Ensure your database is publicly accessible or properly configured for secure access.
   - Allow incoming connections from your Airflow server’s IP in the AWS Security Group settings.

## How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/abdulghaffaransari/Automated-Weather-Data-Workflow.git
   cd Automated-Weather-Data-Workflow
   ```

2. Start Apache Airflow using Docker Compose:
   ```bash
   docker-compose up -d
   ```

3. Trigger the DAG manually or schedule it:
   ```bash
   airflow dags trigger weather_etl_pipeline
   ```

4. Monitor DAG execution in the Airflow UI at `http://localhost:8080`.

## Results
The weather data successfully processed by the pipeline is stored in the `weather` table in AWS RDS. Below is a snapshot of the results:

![Weather Data Results](https://github.com/abdulghaffaransari/Automated-Weather-Data-Workflow/blob/main/Results/Result1.png)

### Table Schema
| Column        | Type      | Description                          |
|---------------|-----------|--------------------------------------|
| `id`          | SERIAL    | Auto-incremented primary key         |
| `latitude`    | FLOAT     | Latitude of the weather location     |
| `longitude`   | FLOAT     | Longitude of the weather location    |
| `temperature` | FLOAT     | Current temperature in Celsius       |
| `windspeed`   | FLOAT     | Wind speed in km/h                   |
| `winddirection` | FLOAT   | Wind direction in degrees            |
| `weathercode` | INT       | Weather condition code               |
| `timestamp`   | TIMESTAMP | Time of data entry                   |

## Future Enhancements
- **Data Visualization**: Integrate dashboards using tools like Tableau or Power BI for real-time weather analysis.
- **Extended API Coverage**: Support multiple locations and weather parameters.
- **Alert System**: Add alerts for extreme weather conditions using email or SMS.
- **Historical Data Analysis**: Archive historical weather data for trend analysis.

## Contributing
Feel free to contribute to this project by submitting issues or pull requests. Follow the [Contributing Guidelines](CONTRIBUTING.md).

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact
For inquiries or support, please contact:
- **Name**: Abdul Ghaffar Ansari
- **GitHub**: [abdulghaffaransari](https://github.com/abdulghaffaransari)
- **LinkedIn**: [Abdul Ghaffar Ansari](https://www.linkedin.com/in/abdulghaffaransari/)
- **Email**: [abdulghaffaransari9@gmail.com](mailto:abdulghaffaransari9@gmail.com)

---

Thank you for exploring the **Automated Weather Data Workflow** project!

