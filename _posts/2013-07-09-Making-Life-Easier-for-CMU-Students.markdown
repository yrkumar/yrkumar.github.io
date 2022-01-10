---
layout: post
title: "Making Life Easier for CMU Students"
date: 2013-07-09 1:00
comments: true
---

Over this past winter break, I was registering for classes using [Carnegie Mellon's Faculty Course Evaluations](http://www.cmu.edu/hub/fce/) (FCE) to help me decide which courses to take. A tool provided by CMU, FCE gathers ratings data by recording student responses to surveys distributed online after each semester ends. These ratings provide a goldmine of information on almost every course offered at CMU. 

As I browsed the site, I realized that it was taking me a while just to find different courses and see how their evaluations matched up (I can't place the blame fully on CMU; FCE seems to be operated by an external company). Although it's a great resource for finding data about courses, FCE wasn't living up to its potential as a powerful course comparison tool... Why? Mostly because of its interface:

![FCE Interface](/static/img/fceInterface.png)

An almost endless drop down menu to narrow options? Semesters worth of ratings data squished into one REALLY big table of values on a single page? I found myself resorting to ctrl-f to find each course I was interested in and then writing down the evaluations as I went so I could do a comprehensive comparison. After almost an hour of frustration, I finally gave up and decided to try and fix it so that I wouldn't have to repeat the process for future semesters.

Using Python and a handy framework called [Scrapy](http://scrapy.org/), I created a simple data crawler to scrape the course evaluations off of FCE and serialize them for easy storage. After running the crawler and gathering the ratings data in a file, I built a front-end search interface with [Flask](http://flask.pocoo.org/) and [Bootstrap](http://twitter.github.io/bootstrap/) to parse search queries that could be made by users, returning the course ratings that matched those queries in a neat and organized table:

![WhichCourse Interface](/static/img/whichCourse.png)

I called the app WhichCourse because I created it to help me choose which courses to take. WhichCourse offers two major advantages over FCE for me:

1. Allows searching for multiple course at once for easy side-by-side comparison
2. Aggregates course evaluations (displayed by semester in FCE) to show a comprehensive rating for each course and professor
3. (Bonus): Provides a slick, bootstrapped interface to view data

Through building WhichCourse, I realized how useless data without organization is. Even though the amount of data in FCE is nowhere near the amount processed by modern day Big Data companies, it still was an immense pain to access when it was unindexed. See [WhichCourse](http://whichcourse.herokuapp.com/) live in action or [browse the source code on Github](https://github.com/yrkumar/which-course).

As a sidenote, I had a great time using Flask and would really recommend it for simple web apps or for prototyping larger Django projects. For example, error handling for WhichCourse (when the user entered a malformed search query) was as simple as utilizing Flask's built-in [Jinja2](http://jinja.pocoo.org/) templating system to display different messages on screen depending on the variety of the error. Here's an example: 

<script src="https://gist.github.com/yrkumar/199d22d3b3088c6a7f4c.js"></script>

Here, the conditionals easily catch malformed search queries and render different HTML templates based on the status of these queries. Aside from an awesome templating system, Flask aslo boasts an awesome built-in debugger and great [documentation](http://flask.pocoo.org/docs/). 

