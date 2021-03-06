mugen
=====

mugen is a microlibrary for implementing infinite scroll on Android.

![alt_tag][_sample_gif]

# Features
- Add infinite scroll to your lists with a few lines of code.
- Configuration allows you to decide how and when to trigger loading. You can even disable load more when all items have been fetched for network usage optimization.
- Supports both `AbsListView` and `RecyclerView`! Which means it's one single library to enable infinite scroll for `ListView`, `GridView` and `RecyclerView` instances.

# Usage

### Basic
```java
    //mCollectionView can be a ListView, GridView, RecyclerView or any instance of AbsListView!
    BaseAttacher attacher = Mugen.with(mCollectionView, new MugenCallbacks() {
            @Override
            public void onLoadMore() {
                /* Will be triggered when the next page has to be loaded.
                *
                * Do your load operation here.
                * Note: this is NOT asynchronous!
                */
            }

            @Override
            public boolean isLoading() {
                /* Return true if a load operation is ongoing. This will
                * be used as an optimization to prevent further triggers
                * if the user scrolls up and scrolls back down before 
                * the load operation finished.
                * 
                * If there is no load operation ongoing, return false
                */
                return isLoading;
            }

            @Override
            public boolean hasLoadedAllItems() {
                /*
                * If every item has been loaded from the data store, i.e., no more items are
                * left to fetched, you can start returning true here to prevent any more
                * triggers of the load more method as a form of optimization.
                *
                * This is useful when say, the data is being fetched from the network
                */
                return false;
            }
        });
        attacher.start();
        
        /* Use this to dynamically turn infinite scroll on or off */
        attacher.setLoadMoreEnabled(true); 
        
        /* Use this to change when the onLoadMore() function is called. 
        * By default, it is called when the scroll reaches 2 items from the bottom */
        attacher.setLoadMoreOffset(4); 
        
        /*
        * mugen uses an internal OnScrollListener to detect and trigger load events.
        * If you need to listen to scroll events yourself, you can set this and 
        * mugen will automatically forward all scroll events to the listener.
        */
        attacher.setOnScrollListener(listener);
```

# Installation
Maven artifact is on the way! Please clone and add as an library module for now.

### Cloning and adding
1. Clone the repository
2. Copy the `library` folder into your project root.
3. Add the line `include ':library'` to your `settings.gradle` file
4. Then, add the line `compile project(':library')` to the `build.gradle` file in your main project.
5. Do a Gradle sync, and you should be good to go!

# License

Copyright 2014 Vinay S Shenoy

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


[_sample_gif]: https://github.com/mipreamble/mugen/blob/development/img_assets/mugen_sample_1.gif
