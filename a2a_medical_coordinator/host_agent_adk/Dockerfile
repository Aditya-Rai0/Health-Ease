# Use a Python 3.12 base image (as required by cardiologist agent)
FROM python:3.12-slim

# Set the working directory
WORKDIR /app

# Copy the dependency files
COPY pyproject.toml uv.lock* ./

# Install dependencies using uv (since uv.lock is present) or pip
# We'll try uv first, then fall back to pip
RUN pip install uv && \
    uv pip install --system . || pip install .

# Copy the rest of your application code
# For cardiologist agent, it's 'app', for host it's 'host'
# Use . . to copy everything in the directory
COPY . .

# Command to run the agent's main file
# This will execute the __main__.py file in the respective directory
# (e.g., app/__main__.py, host/__main__.py, etc.)
# Note: Adjust the path if your structure is different.
# For the 'host_agent_adk' this might be 'python host/agent.py' if it doesn't have a __main__
# But based on your other agents, let's assume they all have a runnable __main__.
#
# For Cardiologist:
# CMD ["python", "app/__main__.py"]
#
# For Neurologist:
# CMD ["python", "__main__.py"]
#
# For Pulmonologist:
# CMD ["python", "__main__.py"]
#
# For Host (assuming it also has a __main__.py to run):
# CMD ["python", "host/__main__.py"]  <-- YOU NEED TO VERIFY THIS
#
# **Please adjust the CMD for each agent based on its entrypoint file**
# Based on your files, the following CMDs are likely correct:

# For cardiologist_agent_langgraph/Dockerfile:
CMD ["python", "app/__main__.py"]

# For neurologist_agent_adk/Dockerfile:
# CMD ["python", "__main__.py"]

# For pulmonologist_agent_crewai/Dockerfile:
# CMD ["python", "__main__.py"]

# For host_agent_adk/Dockerfile: (This is a guess, you may need a __main__.py for it)
# CMD ["python", "host/__main__.py"]