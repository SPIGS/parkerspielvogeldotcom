---
title: "FilterFeed"
date: 2023-09-04T16:50:16-04:00
draft: false
archived: false
personal: true
header_image: /images/projects/filterfeed/filterfeed.png
description: "An alternative frontend to social media, powered by RSS."
tags: ["swift", "ios", "rss"]
source: ""
---

> Updated: December 2023

## About

FilterFeed is a [RSS](https://en.wikipedia.org/wiki/RSS) reader that aims to give the user maximum control over what content they view while attempting to retain the UI/UX of the content for ease of consumption.

FilterFeed started from a personal desire to limit my usage of social media. In short, I believe that social media is hazardous to one's mental health, but despite this, I can still recognize the utility of being able to access and search information in an immediate and user-friendly way. As such, I sought to limit my social media usage not by abstaining from it, but by augmenting how I retrieve and consume it:

 - Increase privacy by separating my consumption of content from the centralization of social media websites.
 - Give myself maximum control over what content is displayed on my screen.
 - Create a user interface that, while easy to use, removes the desire for involuntarily view content ([doomscrolling](https://en.wikipedia.org/wiki/Doomscrolling), [dark patterns](https://en.wikipedia.org/wiki/Dark_pattern), etc.).

These desires have coalesced into this app. While FilterFeed isn't close to being complete, I believe that it is at a far enough point in its development that I am happy to talk about it. I'd estimate that it is just under 50% "done," with the *feed* part of *filter feed* being nearly completed.

## Features

### No APIs

FilterFeed does not use any proprietary APIs to fetch post and feed information. It only uses the RSS and Atom feeds published by sites and then parses and displays the data from there - just like any other RSS reader. I'm predicting other tech companies will be following the lead of Reddit and Twitter by hiking prices on their available APIs, and as such I do not want this app to rely on them.

While this is great in terms of cost and privacy, one may argue that it's not good in terms of interactivity: the lack of APIs users won't be able to interact with content. However, while this is true, I don't think that it is important. As the vast majority of internet userbases comply by the [1% rule](https://en.wikipedia.org/wiki/1%25_rule): *only one percent of users of a site actually contribute to that site*. So, in actuality, I don't think users will miss the ability to interact with content - who wants to argue in YouTube comments, or "dunk" on people on Twitter/X anyway?

All other useful functionality such as saving posts and searching feeds are handled by the app itself.

### No server

All processing for the app is done on-device, this includes fetching posts and displaying them. In addition, all user generated data is stored on device (saved posts, user preferences, etc.). Lastly, the app only makes requests when the user does something: tapping on a post to view it or manually refreshing a feed. The only requests the app makes are GET/FETCH requests. I think that most people underestimate the power of hardware, particularly those of lower-end computers and smartphones. These of devices have a lot of unused computing power hidden by software that can't/won't take advantage of it.

### It looks pretty

I think one of the main problems with most RSS readers is that they are clunky to use and look bad. While this isn't necessarily the fault of those who make them, as I feel those who work on RSS readers mainly want them for their utility, I think the lack of good usability puts off the average person from adopting them. I'm aiming to make the UI/UX of the app more in line with modern UI/UX sensibilities. I've created several different views for different "content types" which allow the content of the feeds to be displayed in way conducive to viewing it. Below you can see some examples:

![A video post example](video_example.PNG "An example of displaying a video and its feed.")

![A text forum post example](forum_post_example.PNG "A text forum post example.")

Additionally, I wrote a converter which turns the HTML of the feed content into a format that can be displayed as rich text on iOS. I did this so there is a consistent feel across the app and to remove formatting from the content. I want the app to look and feel as if it were made by Apple.

![A rich text example](rich_text_example.PNG "A rich text example.")

## Updates

### December 2023

This month, I completed a major rework of FilterFeed. I have completely removed [SwiftSoup](https://github.com/scinfu/SwiftSoup) from the list of dependencies and have written my own HTML parser. SwiftSoup had some weird idiosyncrasies that made it difficult to work with: particularly its parse trees are non-recursive, and getting text node information from tag nodes (and vice versa) was very cumbersome. These issues made it very difficult to do what I needed (converting HTML into Markdown and wrap it in a few data structures).

Surprisingly, this was very straight-forward. The [W3C documentation](https://dev.w3.org/html5/spec-LC/parsing.html) on HTML is very easy to understand. So much so that he documentation is essentially just pseudocode for an actual implementation. However, I did leave out a fair bit of the actual parsing spec - specifically the JavaScript portion since it wasn't needed. So now FilterFeed can display pretty much any HTML content with proper links, images, and formatting all in native SwiftUI views.

I have also sort of "adopted" FeedKit. The original repo hasn't seen any PR merges in about a year and it hasn't seen actual development in about three. I figured since this app is going all-in with RSS and Atom, I might as well bite the bullet and get to know the code base for the most important dependency of my app. I have [forked](https://github.com/SPIGS/FeedKit) the repo and added some changes I needed as well as some of the unmerged PR's from the original repository. I have also updated the notes in the acknowledgements section of the article to reflect this.

Lastly, I've also done some spring-cleaning: I solidified a project structure and cleaned up a lot of my old SwiftUI code. I have also begun to switch over my data backend to SwiftData and I am fairly confident that the oldest version of iOS this app will support is 17. Additionally, I have also switched from SDWebImageSwiftUI to [Kingfisher](https://github.com/onevcat/Kingfisher) for my image downloading and caching.

## Future Plans

1. Finish the feed system (caching, make the parser more robust, etc.)
2. Add filters
3. Finalize look and feel
4. Release on Appstore (?); Release source code (?)

## Acknowledgements and Further Reading

- [AlertToast](https://github.com/elai950/AlertToast/): A library used for Apple-like toast alerts.
- [OpenGraph](https://github.com/satoshi-takano/OpenGraph): A Swift wrapper for the Open Graph protocol; used for some minor scraping of profile/account images.
- [Kingfisher](https://github.com/onevcat/Kingfisher): A web image loading and caching framework.
- [YoutubePlayerKit](https://github.com/SvenTiigi/YouTubePlayerKit): A library to display and play embedded Youtube videos.
- [FeedKit](https://github.com/SPIGS/FeedKit): An RSS, Atom, and JSON feed parser; I have forked the repo so I can continue to add changes if I need any. The original repo can be found [here](https://github.com/nmdias/FeedKit).
- [RSS in Plain English](https://www.youtube.com/watch?v=0klgLsSxGsU)
