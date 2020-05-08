# How to make video contact center using TrueConf Server API
____
## Table of Contents
1. [Pre-configuring TrueConf Server](#pre-configuring-trueconf-server)
1. [Step 1. Obtaining the list of operators](#step-1-obtaining-the-list-of-operators)
1. [Step 2. Selecting an available operator](#step-2-selecting-an-available-operator)
____

TrueConf doesn’t only [provide you with a comfortable and scalable video conferencing system](https://trueconf.com/blog/knowledge-base/get-video-conferencing-system-15-minutes.html), but also enables you to expand its range with the help of [TrueConf Server API](https://developers.trueconf.com/api/server/).

This article covers the detailed algorithm of video contact center deployment based on TrueConf Server. The main idea is to connect a website [guest](https://trueconf.com/blog/wiki/online-user-guest) and an available operator in a private [video conference](https://trueconf.com/what-is-video-conferencing.html). This method uses [WebRTC technology](https://trueconf.com/blog/reviews-comparisons/which-browsers-support-webrtc.html).

:warning: ***WARNING!***
> **The given algorithm and code example is not intended for use in an operational environment. Being deliberately simple, this example is tailored to be used without installing additional software so you can get easily acquainted with TrueConf Server API.**

Both users of [TrueConf Server](https://trueconf.com/products/server/video-conferencing-server.html) and [TrueConf Server Free](https://trueconf.com/products/tcsf/trueconf-server-free.html) can check the working capacity of the described scheme.

As TrueConf Server Free allows only one simultaneous video conference, we do not recommend using it as a full-fledged platform for the video contact center deployment.
____
[:arrow_up:Table of Contents](#table-of-contents)
___

## Pre-configuring TrueConf Server

1. Create a separate group named **Operators** in [TrueConf Server control panel](https://docs.trueconf.com/server/en/admin/web-config#groups-tab) and add users who will accept calls.
1. Configure the [HTTPS connection](https://trueconf.com/blog/knowledge-base/adjust-https-trueconf-server.html) for using WebRTC widget and performing TrueConf Server API requests.

Requests to the TrueConf Server API are used to perform the actions described in the algorithm.
____
[:arrow_up:Table of Contents](#table-of-contents)
___

## Step 1. Obtaining the list of operators

[Obtain the list of all users](https://developers.trueconf.com/api/server/#api-Groups_Users-GetUserList) in the **Operators** group. It is better to do this at each iteration of the algorithm, so you will not miss the moment of adding a new operator to the group.

## Step 2. Selecting an available operator

1. Create the list of online operators (objects [ObjectUser](https://developers.trueconf.com/api/server/#api-Objects-User) [in the list](#Step-1.-Obtaining-the-list-of-operators) will have `status = 1`).
1. Randomly choose one operator from the list. [TrueConf ID](https://trueconf.com/blog/wiki/trueconf-id) of the selected user must differ from the one you specified in step 5 in the previous iteration.
1. If there is no available operator, return to [step 1](#Step-1.-Obtaining-the-list-of-operators) after a short period of time (for example, 10 seconds)
1. Repeat attempts to find an available operator the required number of times (e.g. 3 times) or within a specified period of time (e.g. 30 seconds).


