# LitteLog
Minimalism python logger. Import it directly in one python file, or create a configurable instance as the logger of your whole project.

## Installation
```
pip install littlelog
```

## Usage

### use it in single .py file
```python
from littlelog import logger, debugger

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

### Log file name format
```
log_YYYY-MM-DD_id.txt

e.g: log_2024-09-16_1.txt
```

### Log file content format
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
logger.outputs.append("new/logs/path")   # add log output path
logger.level = "debug"                   # "debug", "info", "warning", "error", "critical"
logger.max_file_size = 5                 # MB
logger.max_files = 20       # Oldest file will be delete when reaching this limitation.
logger.terminal = False                  # Disable logging to terminal.
```



