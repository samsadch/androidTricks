# androidTricks
Trick for android
///news scroll
 final int scrollSpeed = 100;   // Scroll Speed in Milliseconds
            final Handler handler = new Handler();
            final Runnable runnable = new Runnable() {
                int x = 15;        // Pixels To Move/Scroll
                boolean flag = true;
                // Find Scroll Position By Accessing RecyclerView's LinearLayout's Visible Item Position
                int scrollPosition = layoutManager2.findLastCompletelyVisibleItemPosition();
                int arraySize = list.size();  // Gets RecyclerView's Adapter's Array Size

                @Override
                public void run() {
                    if (scrollPosition < arraySize) {
                        if (scrollPosition == arraySize - 1) {
                            flag = false;
                        } else if (scrollPosition <= 1) {
                            flag = true;
                        }
                        if (!flag) {
                            try {
                                // Delay in Seconds So User Can Completely Read Till Last String
                                TimeUnit.SECONDS.sleep(1);
                                offersRcv.scrollToPosition(0);  // Jumps Back Scroll To Start Point
                            } catch (InterruptedException e) {
                                e.printStackTrace();
                            }
                        }
                        // Know The Last Visible Item
                        scrollPosition = layoutManager2.findLastCompletelyVisibleItemPosition();

                        offersRcv.smoothScrollBy(x, 0);
                        handler.postDelayed(this, scrollSpeed);
                    }
                }
            };
            handler.postDelayed(runnable, scrollSpeed);

            handler.postDelayed(runnable,500);
