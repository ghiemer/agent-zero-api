# agent-zero API Integration

This repository extends the [agent-zero](https://github.com/frdel/agent-zero) project by adding a FastAPI interface that allows the usage of the agent via API, enabling its integration with other platforms.

## Overview

The API provides a simple interface for sending tasks to the agent and receiving processed results. This integration makes it easier to interact with the agent remotely and allows for the agent's functionality to be accessed from various external systems.

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/frdel/agent-zero.git
   cd agent-zero
   ```

2. **Update the repository with the new API files**:
   - Add `main_api.py` to the root directory.
   - Update the `requirements.txt` to include the necessary dependencies for FastAPI and Uvicorn:
     ```plaintext
     fastapi==0.95.1
     uvicorn==0.22.0
     ```

3. **Install the dependencies**:
   Make sure you have Python 3.8+ installed. Then, create a virtual environment and install the dependencies:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

4. **Run the FastAPI application**:
   Start the FastAPI application using Uvicorn:
   ```bash
   uvicorn main_api:app --host 0.0.0.0 --port 8000
   ```

## API Endpoints

### `POST /api/execute`

This endpoint is used to execute a task using the configured Agent.

- **Request**:
  - `task` (string): The task to be executed by the Agent.

- **Response**:
  - `status` (string): The status of the task execution, typically "success".
  - `data` (dict): The data containing the response from the Agent.

- **Example**:
  ```bash
  curl -X POST "http://localhost:8000/api/execute" -H "Content-Type: application/json" -d '{"task": "Your task here"}'
  ```

  **Response**:
  ```json
  {
    "status": "success",
    "data": {
      "response": "Task executed"
    }
  }
  ```

## Configuration

The `AgentConfig` class allows for various configurations, which are now accessible through the API:

- **rate_limit_requests**: Number of maximum requests per time window.
- **rate_limit_input_tokens**: Maximum input tokens allowed (set to 0 to disable).
- **rate_limit_output_tokens**: Maximum output tokens allowed (set to 0 to disable).
- **rate_limit_seconds**: Time window for rate limiting (in seconds).
- **max_tool_response_length**: Maximum length of tool responses.
- **code_exec_docker_enabled**: Enable or disable Docker for code execution.
- **code_exec_ssh_enabled**: Enable or disable SSH for code execution.

## Future Enhancements

- **Floating Output via API**: The API will be enhanced in the future to support floating output, allowing for continuous streaming of responses from the agent as they are being processed.

## Running Tests

To run tests, use the following command:
```bash
pytest
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## Contact

If you have any questions, feel free to open an issue or reach out directly.
