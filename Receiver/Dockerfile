FROM arm32v7/python:3.13-bookworm

WORKDIR /app

RUN apt-get update && apt-get install -y \
    build-essential gfortran libatlas-base-dev libopenblas-dev python3-dev \
    && rm -rf /var/lib/apt/lists/*

# Copy backend requirements and install Python packages
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application code
COPY backend/ ./backend/

# Copy the built frontend
COPY ./frontend/dist ./frontend/dist/

COPY pytest.ini pytest.ini
COPY .coveragerc .coveragerc

# Set environment variables
ENV PYTHONPATH=/app

# Command to run the application
CMD ["python", "backend/dronesniffer/main.py"]
