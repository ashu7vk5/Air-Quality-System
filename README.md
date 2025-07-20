# Air-Quality-System
This project is a relational database system designed to monitor and manage air quality in urban areas. It simulates a smart city environment where various sensor devices are deployed across different locations to track pollutants, record maintenance activities, and generate pollution alerts.

PROJECT: CREATE DATABASE IF NOT EXISTS UrbanAirQualityMonitoringSystem;
USE UrbanAirQualityMonitoringSystem;

CREATE TABLE Location (
    location_id INT AUTO_INCREMENT PRIMARY KEY,
    city VARCHAR(100),
    area_name VARCHAR(100),
    manager_name VARCHAR(100)
);

INSERT INTO Location (city, area_name, manager_name) VALUES
('Mumbai', 'Andheri', 'Neha Sharma'),
('Pune', 'Kothrud', 'Rahul Khanna'),
('Delhi', 'Saket', 'Priya Verma'),
('Bangalore', 'Whitefield', 'Amit Rao'),
('Hyderabad', 'Gachibowli', 'Rekha Joshi'),
('Kolkata', 'Salt Lake', 'Ravi Iyer'),
('Chennai', 'T Nagar', 'Anita Desai'),
('Ahmedabad', 'Navrangpura', 'Arun Singh'),
('Jaipur', 'Malviya Nagar', 'Vivek Kapoor'),
('Nagpur', 'Sitabuldi', 'Poonam Saxena'),
('Indore', 'Vijay Nagar', 'Suresh Kumar'),
('Surat', 'Adajan', 'Meera Kulkarni'),
('Lucknow', 'Hazratganj', 'Deepak Sharma'),
('Bhopal', 'MP Nagar', 'Sunita Patil'),
('Thane', 'Ghodbunder Road', 'Rohit Deshmukh');

-- ========================================
-- 2. Table: SensorDevice
-- ========================================
CREATE TABLE SensorDevice (
    sensor_id INT AUTO_INCREMENT PRIMARY KEY,
    device_serial VARCHAR(100),
    pollutant_type VARCHAR(50),
    install_date DATE,
    location_id INT,
    FOREIGN KEY (location_id) REFERENCES Location(location_id)
);

INSERT INTO SensorDevice (device_serial, pollutant_type, install_date, location_id) VALUES
('SNSR001', 'PM2.5', '2025-01-10', 1),
('SNSR002', 'CO2', '2025-01-12', 2),
('SNSR003', 'PM10', '2025-01-15', 3),
('SNSR004', 'NO2', '2025-01-20', 4),
('SNSR005', 'O3', '2025-01-25', 5),
('SNSR006', 'PM2.5', '2025-02-01', 6),
('SNSR007', 'CO2', '2025-02-05', 7),
('SNSR008', 'PM10', '2025-02-10', 8),
('SNSR009', 'NO2', '2025-02-15', 9),
('SNSR010', 'O3', '2025-02-20', 10),
('SNSR011', 'PM2.5', '2025-03-01', 11),
('SNSR012', 'CO2', '2025-03-05', 12),
('SNSR013', 'PM10', '2025-03-10', 13),
('SNSR014', 'NO2', '2025-03-15', 14),
('SNSR015', 'O3', '2025-03-20', 15),
('SNSR016', 'PM2.5', '2025-04-01', 1),
('SNSR017', 'PM2.5', '2025-04-02', 1),
('SNSR018', 'CO2', '2025-04-05', 2);

-- ========================================
-- 3. Table: AirQualityReading
-- ========================================
CREATE TABLE AirQualityReading (
    reading_id INT AUTO_INCREMENT PRIMARY KEY,
    sensor_id INT,
    reading_value DECIMAL(10,2),
    reading_timestamp DATETIME,
    FOREIGN KEY (sensor_id) REFERENCES SensorDevice(sensor_id)
);

INSERT INTO AirQualityReading (sensor_id, reading_value, reading_timestamp) VALUES
(1, 55.6, '2025-06-01 08:00:00'),
(2, 450.3, '2025-06-01 08:05:00'),
(3, 78.9, '2025-06-01 08:10:00'),
(4, 35.5, '2025-06-01 08:15:00'),
(5, 120.1, '2025-06-01 08:20:00'),
(6, 65.4, '2025-06-01 08:25:00'),
(7, 480.2, '2025-06-01 08:30:00'),
(8, 90.8, '2025-06-01 08:35:00'),
(9, 40.2, '2025-06-01 08:40:00'),
(10, 130.6, '2025-06-01 08:45:00'),
(11, 70.5, '2025-06-01 08:50:00'),
(12, 500.7, '2025-06-01 08:55:00'),
(13, 85.2, '2025-06-01 09:00:00'),
(14, 42.8, '2025-06-01 09:05:00'),
(15, 140.3, '2025-06-01 09:10:00');

-- ========================================
-- 4. Table: MaintenanceLog
-- ========================================
CREATE TABLE MaintenanceLog (
    maintenance_id INT AUTO_INCREMENT PRIMARY KEY,
    sensor_id INT,
    maintenance_date DATE,
    technician_name VARCHAR(100),
    notes TEXT,
    FOREIGN KEY (sensor_id) REFERENCES SensorDevice(sensor_id)
);

INSERT INTO MaintenanceLog (sensor_id, maintenance_date, technician_name, notes) VALUES
(1, '2025-05-01', 'Amit Verma', 'Sensor recalibrated'),
(2, '2025-05-03', 'Poonam Singh', 'Filter replaced'),
(3, '2025-05-05', 'Kunal Patel', 'Firmware update'),
(4, '2025-05-07', 'Rita Mehta', 'Battery replaced'),
(5, '2025-05-09', 'Vivek Sharma', 'Sensor cleaned'),
(6, '2025-05-11', 'Amit Verma', 'Filter replaced'),
(7, '2025-05-13', 'Poonam Singh', 'Battery replaced'),
(8, '2025-05-15', 'Kunal Patel', 'Firmware update'),
(9, '2025-05-17', 'Rita Mehta', 'Sensor recalibrated'),
(10, '2025-05-19', 'Vivek Sharma', 'Sensor cleaned'),
(11, '2025-05-21', 'Amit Verma', 'Battery replaced'),
(12, '2025-05-23', 'Poonam Singh', 'Firmware update'),
(13, '2025-05-25', 'Kunal Patel', 'Sensor cleaned'),
(14, '2025-05-27', 'Rita Mehta', 'Battery replaced'),
(15, '2025-05-29', 'Vivek Sharma', 'Sensor recalibrated');

-- ========================================
-- 5. Table: PollutionAlert
-- ========================================
CREATE TABLE PollutionAlert (
    alert_id INT AUTO_INCREMENT PRIMARY KEY,
    sensor_id INT,
    alert_type VARCHAR(100),
    alert_timestamp DATETIME,
    severity VARCHAR(20),
    FOREIGN KEY (sensor_id) REFERENCES SensorDevice(sensor_id)
);

INSERT INTO PollutionAlert (sensor_id, alert_type, alert_timestamp, severity) VALUES
(1, 'High PM2.5 Level', '2025-06-01 08:10:00', 'High'),
(2, 'High CO2 Level', '2025-06-01 08:12:00', 'Medium'),
(3, 'High PM10 Level', '2025-06-01 08:15:00', 'Low'),
(4, 'High NO2 Level', '2025-06-01 08:20:00', 'High'),
(5, 'High O3 Level', '2025-06-01 08:25:00', 'Medium'),
(6, 'High PM2.5 Level', '2025-06-01 08:30:00', 'High'),
(7, 'High CO2 Level', '2025-06-01 08:35:00', 'Low'),
(8, 'High PM10 Level', '2025-06-01 08:40:00', 'Medium'),
(9, 'High NO2 Level', '2025-06-01 08:45:00', 'High'),
(10, 'High O3 Level', '2025-06-01 08:50:00', 'Low'),
(11, 'High PM2.5 Level', '2025-06-01 08:55:00', 'Medium'),
(12, 'High CO2 Level', '2025-06-01 09:00:00', 'High'),
(13, 'High PM10 Level', '2025-06-01 09:05:00', 'Low'),
(14, 'High NO2 Level', '2025-06-01 09:10:00', 'Medium'),
(15, 'High O3 Level', '2025-06-01 09:15:00', 'High');

-- ========================================
-- INTERMEDIATE LEVEL QUERIES
-- ========================================

-- 1. Total sensors per city
SELECT l.city, COUNT(s.sensor_id) AS total_sensors
FROM SensorDevice s
JOIN Location l ON s.location_id = l.location_id
GROUP BY l.city;


-- 2. Sensors with AND without maintenance in May 2025 (more reliable)
SELECT s.device_serial, 
       CASE WHEN m.maintenance_id IS NULL THEN 'No' ELSE 'Yes' END AS has_maintenance_in_may
FROM SensorDevice s
LEFT JOIN MaintenanceLog m 
  ON s.sensor_id = m.sensor_id AND MONTH(m.maintenance_date) = 5;

-- 3. Top 5 highest pollution readings
SELECT a.sensor_id, s.device_serial, a.reading_value
FROM AirQualityReading a
JOIN SensorDevice s ON a.sensor_id = s.sensor_id
ORDER BY a.reading_value DESC
LIMIT 5;

-- 4. Count of alerts by severity
SELECT severity, COUNT(*) AS total_alerts
FROM PollutionAlert
GROUP BY severity;

-- 5. Average reading by pollutant type
SELECT s.pollutant_type, ROUND(AVG(a.reading_value), 2) AS avg_value
FROM AirQualityReading a
JOIN SensorDevice s ON a.sensor_id = s.sensor_id
GROUP BY s.pollutant_type;

-- 6. Last maintenance date per sensor
SELECT s.device_serial, MAX(m.maintenance_date) AS last_maintenance
FROM SensorDevice s
JOIN MaintenanceLog m ON s.sensor_id = m.sensor_id
GROUP BY s.device_serial;

-- 7. All high severity alerts
SELECT * FROM PollutionAlert
WHERE severity = 'High';

-- 8. Area-wise high severity alerts
SELECT l.area_name, COUNT(p.alert_id) AS high_alerts
FROM PollutionAlert p
JOIN SensorDevice s ON p.sensor_id = s.sensor_id
JOIN Location l ON s.location_id = l.location_id
WHERE p.severity = 'High'
GROUP BY l.area_name;

-- 9. Sensors triggering more than 1 alert
SELECT s.device_serial, COUNT(p.alert_id) AS alert_count
FROM PollutionAlert p
JOIN SensorDevice s ON p.sensor_id = s.sensor_id
GROUP BY s.device_serial
HAVING COUNT(p.alert_id) > 1;

-- 10. Sensors with average reading above 100
SELECT s.device_serial, ROUND(AVG(a.reading_value), 2) AS avg_reading
FROM AirQualityReading a
JOIN SensorDevice s ON a.sensor_id = s.sensor_id
GROUP BY s.device_serial
HAVING avg_reading > 100;


-- 11. Latest reading timestamp per sensor
SELECT s.device_serial, MAX(a.reading_timestamp) AS latest_reading
FROM AirQualityReading a
JOIN SensorDevice s ON a.sensor_id = s.sensor_id
GROUP BY s.device_serial;

-- 12. Sensors installed in 2025
SELECT device_serial, install_date
FROM SensorDevice
WHERE YEAR(install_date) = 2025;


-- 13. Alerts by type
SELECT alert_type, COUNT(*) AS total_alerts
FROM PollutionAlert
GROUP BY alert_type;

-- 14. Cities with at 2 PM2.5 sensors
SELECT l.city, COUNT(*) AS pm25_sensors
FROM SensorDevice s
JOIN Location l ON s.location_id = l.location_id
WHERE s.pollutant_type = 'PM2.5'
GROUP BY l.city
HAVING COUNT(*) >= 2;

-- 15. Sensors with no alert record
SELECT s.device_serial
FROM SensorDevice s
LEFT JOIN PollutionAlert p ON s.sensor_id = p.sensor_id
WHERE p.alert_id IS NULL;


Key insights derived from your Urban Air Quality Monitoring System that can provide **strategic direction** for environmental agencies, smart city planners, or health-focused organizations:

-- These insights turn raw sensor data into actionable intelligence, helping organizations take data-driven decisions toward cleaner, healthier cities. If needed, I can also help convert these insights into dashboard KPIs or policy recommendation reports.

Features
5 Normalized Tables: Location, SensorDevice, AirQualityReading, MaintenanceLog, PollutionAlert
Data for 15 cities and 15 sensors
15+ Intermediate SQL Queries using JOIN, GROUP BY, HAVING, and aggregates
Clean schema design suitable for extensions (dashboards, APIs, ML)
1. Pollution Hotspots
Identifies areas with highest average pollution readings or frequent alerts.
✅ Use for targeted emission controls and public health notifications.

2. Pollutant Type Mapping
Shows city-wise trends for PM2.5, CO2, NO2, and O3.
✅ Helps design pollutant-specific intervention policies.

3. Sensor Maintenance Gaps
Finds sensors lacking regular servicing or with outdated readings.
✅ Enables proactive maintenance scheduling and reduces system failures.

4. Alert Severity Analysis
Clusters of high-severity alerts signal public health risk zones.
✅ Supports health advisories and urban policy adjustments.

5. Infrastructure Coverage
Highlights regions with fewer sensors or pollutant blind spots.
✅ Guides future sensor deployments for full city coverage.

6. Predictive Maintenance
Analyzes historical logs to anticipate recurring sensor issues.
✅ Reduces downtime and improves sensor reliability.

🚀 Ideal Use Cases
SQL & Data Analytics Projects
IoT Smart City Solutions
Environmental Monitoring Initiatives
Academic or Capstone Submissions

 


