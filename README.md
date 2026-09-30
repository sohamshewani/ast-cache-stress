### Overview
The `ast-cache-stress` repository contains a multi-component CLI utility designed to perform various tasks related to static code analysis, local cache emulation, and API stress testing. The tool is built using Python and leverages several libraries for enhanced functionality, including `astroid` for static code analysis, `aiosqlite` for local cache management, and `rich` for rich console output.

### Installation
To install the tool, use the following command:
```bash
pip install -e .
```

### Core Components
1. **AST-Based Static Dead Code Analyzer**
   - Analyzes Python code to identify dead code using the `astroid` library.
2. **SQLite-Backed Local Redis Cache Emulator**
   - Emulates a local Redis cache using SQLite to store and retrieve key-value pairs.
3. **Async Concurrent API Stress Tester**
   - Tests the performance and behavior of APIs under heavy concurrent load using asynchronous programming.

### Usage

#### Static Dead Code Analyzer
To analyze a Python file for dead code, use the following command:
```bash
ast-cache-stress analyze --file path/to/your/file.py
```

#### Local Redis Cache Emulator
To emulate a local Redis cache, use the following command:
```bash
ast-cache-stress cache --key my_key --value my_value
ast-cache-stress cache --key my_key --get
ast-cache-stress cache --key my_key --delete
```

#### API Stress Tester
To test the performance of an API, use the following command:
```bash
ast-cache-stress stress --url https://api.example.com --count 100 --interval 1
```

### Architecture
- **Core Code**: The core functionality for AST-based analysis, cache emulation, and API stress testing.
- **CLI Code**: Handles user input and provides rich terminal output using the `rich` library.
- **Test Code**: Pytest suite to ensure the core components are functioning as expected.

### Technical Details
- **Core Code**: `src/core.py`
- **CLI Code**: `src/cli.py`
- **Test Code**: `tests/test_core.py`

### Example Tests
```python
# tests/test_core.py
import pytest
from ast_cache_stress.src.core import analyze_code, emulate_redis_cache, stress_test_api

@pytest.mark.parametrize('file_path', ['tests/sample_code.py'])
def test_analyze_code(file_path: str):
    result = analyze_code(file_path)
    assert result == {'dead_code': [], 'live_code': ['def main():', '    print("Hello, world!")']}

def test_emulate_redis_cache():
    key = 'test_key'
    value = 'test_value'
    emulate_redis_cache(key, value)
    assert emulate_redis_cache(key, get=True) == value

def test_stress_test_api():
    url = 'https://api.example.com'
    count = 10
    interval = 1
    results = stress_test_api(url, count, interval)
    assert len(results) == count
```

### Contributing
Contributions are welcome! Please read the [CONTRIBUTING.md](CONTRIBUTING.md) file for more information on how to contribute.

### License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.