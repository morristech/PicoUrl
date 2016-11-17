# PicoUrl
Create tiny shareable URLs that can be parsed back into the original URLs

[![Build Status](https://travis-ci.org/Commit451/PicoUrl.svg?branch=master)](https://travis-ci.org/Commit451/PicoUrl)
[![](https://jitpack.io/v/Commit451/PicoUrl.svg)](https://jitpack.io/#Commit451/PicoUrl)

Who has time to create a backend tiny url parser? Why not leverage one that already exists, such as [TinyUrl](http://tinyurl.com/). The only problem is, a lot of times, you probably want to allow for deep links into your app using tiny urls, but for the best of reasons, do not want to register for all urls starting with `http://tinyurl.com`

The solution is one that is interesting. This library takes a url that you would want to shorten, such as `http://commit451.github.io/linkipedia?query=hi&source=twitter&unicorns=true` and turn it into something like `http://commit451.com/j6zlwzh`, which makes far more sense to register deep links for.

# Usage
```java
//Initialize an instance of PicoUrl
picoUrl = new PicoUrl.Builder()
                .baseUrl("http://mysite.com")
                .build();
//Create a url that your app understands and can parse:
Uri shareUrl = Uri.parse("http://mysite.com");
shareUrl = shareUrl.buildUpon()
        .appendQueryParameter("id", someId))
        .appendQueryParameter("referer", userId))
        .appendQueryParameter("unicorns", "true"))
        .build();
//Turns http://mysite.com?id=someId&referer=userId&unicorns=true
//into http://mysite.com?tinyUrl=j71a1h
picoUrl.generate(shareUrl).subscribeOn(Schedulers.newThread())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new Subscriber<Uri>() {
                    @Override
                    public void onCompleted() {
                    }

                    @Override
                    public void onError(Throwable e) {
                        e.printStackTrace();
                        //Alert your user!
                    }

                    @Override
                    public void onNext(Uri url) {
                        //Send the link to the other user, or post it on the internet for others to click!
                    }
                });

//When receiving the shortened url:
picoUrl.parse(shortenedUrl).subscribeOn(Schedulers.newThread())
                    .observeOn(AndroidSchedulers.mainThread())
                    .subscribe(new Subscriber<Uri>() {
                        @Override
                        public void onCompleted() {
                        }

                        @Override
                        public void onError(Throwable e) {
                            e.printStackTrace();
                            //Alert your user!
                        }

                        @Override
                        public void onNext(Uri url) {
                            String id = url.
                        }
                    });
```

# About
This library was created for [Linkipedia](https://play.google.com/store/apps/details?id=com.commit451.linkipedia), an app where you try to beat your friends from one Wikipedia page to another.

License
--------

    Copyright 2016 Commit 451

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
