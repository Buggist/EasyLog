# LitteLog
Minimalism python logger. Import it directly in one python file, or create a configurable instance as the logger of your whole project.

## Installation
```
pip install littlelog
```

## Usage

### Use it in single *.py* file
```python
from littlelog import logger, debugger

# Config log output path
logger.outputs.append("logs/")

# manually log - five levels in total
logger.debug("Log a debug information.")
logger.info("Log a information.")
logger.warning("Log a warning.")
logger.error("Log a error.")
logger.critical("Log a critical error.")

# function decorator
@debugger
def your_function():
    # Debugger will automatically log the start and end status of this function on 'debug' level,
    # - and log error on 'error' level.
    ...
    return "Hello!"

@debugger
def div_func(a, b):
    return a / b

your_function()
div_func(3, 0)
```

### Use it as logger of whole project
First, create a independent logger module for your project.
*project_logger.py*
```python
import littlelog

# Log files will be output to "where/your/logs/output".
# Config of your project logger module saves at "where/ProjectConfig/file/stay"
logger = littlelog.new("where/your/logs/output", "where/ProjectConfig/file/stay")

debugger = logger.log_decorator
```
And import ***project_logger.py*** instead of ***littlelog*** to fetch logger in any file of current project,
they will share exactly 1 logger and same configurations.

All changes of configuration will be saved.

### Log file name format
```
log_YYYY-MM-DD_id.txt
```
e.g: log_2024-09-16_1.txt

### Log file content example
```
2024-09-16 10:49:00,012 - DEBUG
Log a debug information.

2024-09-16 10:49:00,012 - INFO
Log a information.

2024-09-16 10:49:00,012 - WARNING
Log a warning.

2024-09-16 10:49:00,012 - ERROR
Log a error.

2024-09-16 10:49:00,012 - CRITICAL
Log a critical error.

2024-09-16 10:49:00,012 - DEBUG
Function Start: your_function

2024-09-16 10:49:00,012 - DEBUG
Function complete: your_function, 
  return as Hello!

2024-09-16 10:49:00,012 - DEBUG
Function Start: div_func

2024-09-16 10:49:00,012 - ERROR
Function execution error: div_func, Messages: division by zero
Traceback (most recent call last):
  File "C:\project\littlelog\littlelog.py", line 377, in wrapper
    result = func(*args, **kwargs)
             ^^^^^^^^^^^^^^^^^^^^^
  File "C:\project\littlelog\example\test.py", line 22, in div_func
    return a / b
           ~~^~~
ZeroDivisionError: division by zero
```

### Configurations
```python
# add log output path
logger.outputs.append("new/logs/path")   # (default is [])

# "debug", "info", "warning", "error", "critical"
logger.level = "debug"                   # (default is "debug")

# MB           
logger.max_file_size = 5                 # (default is 2)

# Oldest file will be delete when reaching this limitation.
logger.max_files = 20                    # (default is 10)

# Disable logging to terminal.
logger.terminal = False                  # (default is True)
```



