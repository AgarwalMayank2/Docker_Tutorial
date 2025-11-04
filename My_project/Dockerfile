# Import a base image
FROM python:3.11-slim

# Define a workdir where all our files will be kept and we will be working in it
WORKDIR /docker_project

# Copy the dependencies
COPY requirements.txt .

# Install the dependencies
RUN pip install -r requirements.txt

# Copy source codes
COPY . .
# The first . is for source(host) full folder and second . is for docker working directory.
# As we are currently working in a directory in our docker, we dont need to define particular folder.

# Now run the project
CMD ["python", "main.py"]