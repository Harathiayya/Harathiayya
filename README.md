import psutil
import logging
import os

# Configure logging
logging.basicConfig(filename='system_health.log', level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')

# Define thresholds
CPU_THRESHOLD = 80  # Percentage
MEMORY_THRESHOLD = 80  # Percentage
DISK_THRESHOLD = 90  # Percentage

def check_cpu_usage():
    cpu_usage = psutil.cpu_percent()
    if cpu_usage > CPU_THRESHOLD:
        logging.warning(f"High CPU Usage: {cpu_usage}%")
        print(f"Alert: High CPU Usage: {cpu_usage}%")
    else:
        logging.info(f"CPU Usage: {cpu_usage}%")

def check_memory_usage():
    memory = psutil.virtual_memory()
    memory_usage = memory.percent
    if memory_usage > MEMORY_THRESHOLD:
        logging.warning(f"High Memory Usage: {memory_usage}%")
        print(f"Alert: High Memory Usage: {memory_usage}%")
    else:
        logging.info(f"Memory Usage: {memory_usage}%")

def check_disk_usage():
    disk = psutil.disk_usage('/')
    disk_usage = disk.percent
    if disk_usage > DISK_THRESHOLD:
        logging.warning(f"High Disk Usage: {disk_usage}%")
        print(f"Alert: High Disk Usage: {disk_usage}%")
    else:
        logging.info(f"Disk Usage: {disk_usage}%")

def check_running_processes():
    processes = [p.info for p in psutil.process_iter(attrs=['pid', 'name'])]
    logging.info(f"Running Processes: {processes}")

if __name__ == "__main__":
    check_cpu_usage()
    check_memory_usage()
    check_disk_usage()
    check_running_processes()

