
# Lesson 02. The benefits of offline first

Udacity Grow with Google Scholarship

Brendon Smith

br3ndonland

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Lesson](#lesson)
  - [2.01. Intro](#201-intro)
  - [2.02. The Problem](#202-the-problem)
  - [2.03. The Benefits of Offline First](#203-the-benefits-of-offline-first)
  - [2.04. Quiz: What Can Slow Us Down](#204-quiz-what-can-slow-us-down)
  - [2.05. Quiz: What Does Online First Look Like](#205-quiz-what-does-online-first-look-like)
  - [2.06. Quiz: What Are Ways To Be Offline First](#206-quiz-what-are-ways-to-be-offline-first)
  - [2.07. Introducing the Demo App](#207-introducing-the-demo-app)
  - [2.08. Quiz: Installing the Demo App](#208-quiz-installing-the-demo-app)
  - [2.09. Quiz: Running the Demo App](#209-quiz-running-the-demo-app)
  - [2.10. Exploring the Demo Apps Code](#210-exploring-the-demo-apps-code)
  - [2.11. Quiz: Changing Connection Types](#211-quiz-changing-connection-types)
  - [2.12. Quiz: Testing Lie Fi Mode](#212-quiz-testing-lie-fi-mode)
  - [2.13. Introducing Service Worker](#213-introducing-service-worker)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## Lesson

### 2.01. Intro
### 2.02. The Problem
### 2.03. The Benefits of Offline First
### 2.04. Quiz: What Can Slow Us Down
### 2.05. Quiz: What Does Online First Look Like
### 2.06. Quiz: What Are Ways To Be Offline First
### 2.07. Introducing the Demo App
### 2.08. Quiz: Installing the Demo App

* Node installed:
	```bash
	$ node --version
	v8.7.0
	```
* Clone and run app
	```
	$ cd <path>
	$ git clone https://github.com/jakearchibald/wittr
	$ npm install
	$ npm update
	$ npm run serve
	```
* Navigate to http://localhost:8888/ for the app and http://localhost:8889/ for the settings.
* I was able to successfully get the app running.
* **Note: the wittr app repo is ~230 MB and contains thousands of files. I noticed the files syncing through my Dropbox, and moved the repo out of Dropbox.**


### 2.09. Quiz: Running the Demo App

### 2.10. Exploring the Demo Apps Code

* wittr makes an HTTP request via the browser's HTTP cache.
* If no match in HTTP cache, continues on to internet server.
* wittr also requests some JavaScript. This opens a **web socket**, a persistent connection that continually streams newer posts from the server.


### 2.11. Quiz: Changing Connection Types
### 2.12. Quiz: Testing Lie Fi Mode
### 2.13. Introducing Service Worker