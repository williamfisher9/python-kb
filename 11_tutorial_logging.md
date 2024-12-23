# LOGGING
The logging module offers a full featured and flexible logging system. At its simplest, log messages are sent to a file or to sys.stderr
```
import logging
logging.debug('Debugging information')
logging.info('Informational message')
logging.warning('Warning:config file %s not found', 'server.conf')
logging.error('Error occurred')
logging.critical('Critical error -- shutting down')
```
- Other output options include routing messages through email, datagrams, sockets, or to an HTTP Server.
- New filters can select different routing based on message priority: DEBUG, INFO, WARNING, ERROR, and CRITICAL.
- The logging system can be configured directly from Python or can be loaded from a user editable configuration file for customized logging without altering the application.
