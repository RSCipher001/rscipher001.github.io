+++
categories = ["termux", "wfuzz", "hacking"]
date = "2021-04-04"
description = "In this post we will see how to install wfuzz in Termux"
title = "Install WFuzz in Termux"
+++

WFuzz is a web fuzzing tool and I really like it, I was trying to install it in Termux so I can use my mobile for running WFuzz. Let's do it.

## Install Dependencies

Open Termux and run the following command it will install all the dependencies.

```
pkg i python python-dev openssl openssl-dev curl clang libcrypt libcrypt-dev libcurl libcurl-dev
```

Run the following command to set ssl library or it won't work.
```
export PYCURL_SSL_LIBRARY=openssl
```

Now run this last command and we are done
```
pip install wfuzz
```

Congratulations, you have successfully installed wfuzz on Termux.