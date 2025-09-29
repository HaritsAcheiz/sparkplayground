The following section constitutes the operational documentation required to set up and initiate the Spark Cluster Playground.

A. Project Title and Description

Project Title: Spark Cluster Playground: Local Distributed Computing with Docker and PySpark

Description: This project establishes a local, fully functional Apache Spark cluster playground. Utilizing Docker and Python, it is meticulously designed for hands-on experience in distributed computing, interactive development via Jupyter Lab, and critical database integration with PostgreSQL. This lightweight, local setup accurately mirrors the architecture and constraints of real-world Spark jobs, providing a protected environment for developers to test, learn, and implement performance optimizations like caching and memory tuning.  

B. Features and Capabilities

The cluster playground provides a comprehensive set of features tailored for data engineering practice:

    Full Cluster Architecture: The environment is deployed as a working Spark cluster, including a Master node responsible for orchestration and coordination, and two Worker nodes responsible for execution.   

Interactive Development: Jupyter Lab is integrated with a dedicated Spark kernel, allowing for iterative, interactive execution of PySpark code.  

Database Integration: Provides seamless integration for practicing data reads and writes with a PostgreSQL database via the industry-standard JDBC protocol.  

Optimization Blueprint: Serves as a testbed for advanced performance concepts, including experimentation with strategic DataFrame partitioning, implementing caching strategies, utilizing broadcast variables, and tuning executor memory settings.  

C. Prerequisites and System Requirements Checklist

Successful deployment requires adherence to the following dependencies and hardware recommendations:

Software Requirements:

    Containerization: Docker and Docker Compose must be installed and operational.

    Programming Language: Python 3.12 (or a compatible version) is required.

    JVM: OpenJDK-17-jdk must be installed locally on the host machine.   

Dependencies: Basic working knowledge of SQL and Python is necessary for running the validation tests.  

Critical Hardware Note:
Given that the setup runs three active containers (Master and two Workers) plus the local Jupyter Lab environment, a minimum of 8GB of RAM is strongly recommended for stable, simultaneous operation.

D. Installation and Setup Guide

The following steps detail the necessary procedures for preparing the local environment and installing the required components.

1. Directory and Environment Creation

The project structure requires a dedicated directory and a location for sharing files between the host machine and the Docker containers.
Bash

mkdir sparkplayground
cd sparkplayground
mkdir shared-data

2. Local Python Environment Setup

The host environment requires a virtual environment for dependency management, ensuring the necessary Python packages, including PySpark and Jupyter Lab, are isolated.
Bash

python3 -m venv venv
source venv/bin/activate

3. Defining Dependencies and Installing Libraries

A requirements.txt file (content not explicitly defined in the source, but presumed to contain pyspark, jupyterlab, and database interface tools like psycopg2) must be created. The system requires specific system libraries before Python packages can be installed.
Bash

# Install system-level PostgreSQL libraries, often required for database API compilation
sudo apt install libpq-dev

# Install Python dependencies defined in requirements.txt
pip install -r requirements.txt

# Install a dedicated kernel for the virtual environment
python3 -m ipykernel install --user --name=spark

4. Java and JDBC Driver Management

Since Spark is fundamentally a JVM application, the host machine executing the PySpark driver requires a Java runtime environment. Furthermore, database connectivity necessitates the physical presence of the PostgreSQL JDBC driver.

    Host Java Installation:
    Bash

sudo apt install openjdk-17-jdk

JDBC Driver Acquisition: Download the binary JAR file for the PostgreSQL JDBC Driver. The specific version mentioned in the project architecture is postgresql-42.7.5.jar.  

Driver Placement: The downloaded JAR file must be copied into the designated shared volume folder:
Bash

    Copy postgresql-42.7.5.jar into shared-data folder

E. Cluster Launch and Basic Validation

1. Docker Compose Execution

Assuming the docker-compose.yaml file (defining the services for spark-master, spark-worker-1, spark-worker-2, and postgres) is correctly configured in the sparkplayground directory, the cluster is initialized using the detached mode command:
Bash

docker-compose up -d

2. System Verification

Immediately after launch, the state of the cluster should be verified using the Spark Web User Interface (UI).

    Action: Visit the Spark UI.

    URL: http://localhost:8080

    Expected Outcome: The UI dashboard should clearly display the status of the cluster, specifically confirming the presence and readiness of two operational worker nodes. 1   
