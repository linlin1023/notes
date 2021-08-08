# JUL

* how to create thread
    * extends Thread 
    * implement Runnable (usually)
  
* start method
* stop is deprecated, it is not safe, if a thread is running, you call stop, the thread will not release the locks it hold, and it will not save the stop status for the thread, if other thread want to use this status, it will cause unexpected exception in other thread,so for the stop function you need to implement by your self.
```java
    public static void main(String[] args) throws InterruptedException {
        StopThread thread = new StopThread() ;
        thread.start();
        Thread.sleep(1000L);
        thread.stop();  
        while (thread.isAlive()){}
        thread.print();
    }
    private static class  StopThread extends Thread {
        private int x = 0;
        private int y = 0;

        @Override
        public void run(){
            synchronized (this) { //atom, both failed or both success
                ++x;
                try{
                    Thread.sleep(3000l);
                }catch (InterruptedException e){
                    e.printStackTrace();
                }
                ++y;
            }
        }
        public void print(){
            System.out.println("x = " + x + ", y = " + y);
        }
    }
```


* how to implement a safe stop
  * define a stop flag inside class
  * implement a method that check the stop flag and return if the thread is still running
  ```java
  class MyRunnable implements Runnable{
    private boolean doStop = false;
    public synchronized void doStop(){
        this.doStop = true; // before this, you could release locks this thread is holding
    }
    private synchronized boolean keepRunning() {
        return this.doStop == false;
    }
    @Override
    public void run() {
        while(keepRunning()){
            System.out.println(Thread.currentThread().getName());
            System.out.println("Running");
        }
    }
    ```

* terminal  interrupt pause
    * pause: 
        * Thread.sleep() (not release lock it's holding)
    * interrupt:
        * interrupt(): Thread instance method, must be invoked by other thread when obtained the instance. It basically just change the interruption status inside the thread instance.
        * interrupt(): when the thread instance sleep or wait, it will throw InterruptedException
        * All the method that will throw InterruptedException like wait, sleep and join, they all keep checking interruption status inside their method body.
        * Thread.interrupted(): only invoked inside current thread, it returns current interrupt status and set it to false;
        * isInterrupted() check the interrupt status of the thread instance 



