# MULTI-THREADING
- Threading is a technique for decoupling tasks which are not sequentially dependent.
- Threads can be used to improve the responsiveness of applications that accept user input while other tasks run in the background.
- A related use case is running I/O in parallel with computations in another thread.
- Python has a high level threading module which can run tasks in background while the main program continues to run:
  ```
  import threading, zipfile
  
  class AsyncZip(threading.Thread):
      def __init__(self, infile, outfile):
          threading.Thread.__init__(self)
          self.infile = infile
          self.outfile = outfile
  
      def run(self):
          f = zipfile.ZipFile(self.outfile, 'w', zipfile.ZIP_DEFLATED)
          f.write(self.infile)
          f.close()
          print('Finished background zip of:', self.infile)
  
  background = AsyncZip('mydata.txt', 'myarchive.zip')
  background.start()
  print('The main program continues to run in foreground.')
  
  background.join()    # Wait for the background task to finish
  print('Main program waited until background was done.')
  ```
- The principal challenge of multi-threaded applications is coordinating threads that share data or other resources.
- To that end, the threading module provides a number of synchronization primitives including locks, events, condition variables, and semaphores.
- The preferred approach to task coordination is to concentrate all access to a resource in a single thread and then use the queue module to feed that thread with requests from other threads.
- Applications using Queue objects for inter-thread communication and coordination are easier to design, more readable, and more reliable.
