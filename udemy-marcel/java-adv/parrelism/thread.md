# Below is blocking call

  public Product retrieveProductDetails(String productId) {
        stopWatch.start();

        ProductInfo productInfo = productInfoService.retrieveProductInfo(productId); // blocking call
        Review review = reviewService.retrieveReviews(productId); // blocking call

        stopWatch.stop();
        log("Total Time Taken : "+ stopWatch.getTime());
        return new Product(productId, productInfo, review);
    }

    Paralley(2sec to 1sec)
public Product retrieveProductDetails(String productId) throws InterruptedException {
        stopWatch.start();
        ProductInfoRunnable productInfoRunnable = new ProductInfoRunnable(productId);
        ReviewRunnable reviewRunnable = new ReviewRunnable(productId);

        Thread productInfoThread = new Thread(productInfoRunnable);
        Thread reviewThread = new Thread(reviewRunnable);

        productInfoThread.start();
        reviewThread.start();

        productInfoThread.join();
        reviewThread.join();

        stopWatch.stop();
        log("Total Time Taken : "+ stopWatch.getTime());
        return new Product(productId, productInfoRunnable.productInfo, reviewRunnable.review);
    
    https://github.com/dilipsundarraj1/parallel-asynchronous-using-java/blob/final/src/main/java/com/learnjava/thread/ProductServiceUsingThread.java

    # 2nd way - by executor servicxe for clean code 

    u have to shutdown executor service o/w the program wiull be up and running

    https://github.com/dilipsundarraj1/parallel-asynchronous-using-java/blob/final/src/main/java/com/learnjava/executor/ProductServiceUsingExecutor.java

    executor.submit(task): You submit a Callable (or Runnable) to the ExecutorService, which returns a Future object.
future.get(long timeout, TimeUnit unit): This is the key method.
timeout: The maximum time to wait for the task to complete.
unit: The unit of time for the timeout (e.g., TimeUnit.SECONDS, TimeUnit.MILLISECONDS).
TimeoutException: If the task does not complete within the specified timeout, a TimeoutException is thrown. You should catch this exception and handle the timeout scenario, such as logging the event or canceling the task.
future.cancel(true): If a TimeoutException occurs and you no longer need the task to continue running, you can call cancel(true) on the Future. This attempts to interrupt the thread executing the task. The task itself needs to be designed to respond to interruptions for this to be effective.

Workstealing - some other thread steal task of other thread to distribute task properly

Hands on - (forkjoin)

https://github.com/dilipsundarraj1/parallel-asynchronous-using-java/blob/final/src/main/java/com/learnjava/forkjoin/ForkJoinUsingRecursion.java

   protected List<String> compute() {

        if (this.inputList.size() <= 1) {
            List<String> resultList = new ArrayList<>();
            inputList.forEach(name -> resultList.add(transform(name)));
            return resultList;
        }
        int midPoint = inputList.size() / 2;
        ForkJoinTask<List<String>> leftInputList = new ForkJoinUsingRecursion(inputList.subList(0, midPoint)) //left side of the list
                .fork(); // 1. asynchronously arranges this task in the deque,
        inputList = inputList.subList(midPoint, inputList.size()); //right side of the list
        List<String> rightResult = compute();
        List<String> leftResult = leftInputList.join();
        log("leftResult : "+ leftResult);
        leftResult.addAll(rightResult);
        return leftResult;
    }
