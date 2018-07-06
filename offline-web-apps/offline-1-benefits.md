# The benefits of offline first

<a href="https://www.udacity.com/">
  <img src="https://s3-us-west-1.amazonaws.com/udacity-content/rebrand/svg/logo.min.svg" width="300" alt="Udacity logo">
</a>

[Offline Web Applications by Google course](https://www.udacity.com/course/offline-web-applications--ud899) lesson 1/3

Udacity Google Mobile Web Specialist Nanodegree program part 2 lesson 16

Udacity Grow with Google Scholarship challenge course lesson 02

Brendon Smith

br3ndonland

## Table of Contents <!-- omit in toc -->

- [Lesson](#lesson)
  - [1.01. Intro](#101-intro)
  - [1.02. The Problem](#102-the-problem)
  - [1.03. The Benefits of Offline First](#103-the-benefits-of-offline-first)
  - [1.04. Quiz: What Can Slow Us Down](#104-quiz-what-can-slow-us-down)
  - [1.05. Quiz: What Does Online First Look Like](#105-quiz-what-does-online-first-look-like)
  - [1.06. Quiz: What Are Ways To Be Offline First](#106-quiz-what-are-ways-to-be-offline-first)
  - [1.07. Introducing the Demo App](#107-introducing-the-demo-app)
  - [1.08. Quiz: Installing the Demo App](#108-quiz-installing-the-demo-app)
  - [1.09. Quiz: Running the Demo App](#109-quiz-running-the-demo-app)
  - [1.10. Exploring the Demo Apps Code](#110-exploring-the-demo-apps-code)
  - [1.11. Quiz: Changing Connection Types](#111-quiz-changing-connection-types)
  - [1.12. Quiz: Testing Lie Fi Mode](#112-quiz-testing-lie-fi-mode)
  - [1.13. Introducing Service Worker](#113-introducing-service-worker)

## Lesson

### 1.01. Intro

### 1.02. The Problem

### 1.03. The Benefits of Offline First

### 1.04. Quiz: What Can Slow Us Down

### 1.05. Quiz: What Does Online First Look Like

### 1.06. Quiz: What Are Ways To Be Offline First

### 1.07. Introducing the Demo App

### 1.08. Quiz: Installing the Demo App

- Node installed:

  ```shell
  $ node --version
  v8.7.0
  ```

- Clone and run app

  ```shell
  $ cd <path>
  $ git clone https://github.com/jakearchibald/wittr
  $ npm install
  $ npm update
  $ npm run serve
  ```

- Navigate to http://localhost:8888/ for the app and http://localhost:8889/ for the settings.
- I was able to successfully get the app running.
- **The wittr app repo is ~230 MB and contains thousands of files. I noticed the files syncing through my Dropbox, and moved the repo out of Dropbox.**

### 1.09. Quiz: Running the Demo App

### 1.10. Exploring the Demo Apps Code

- wittr makes an HTTP request via the browser's HTTP cache.
- If no match in HTTP cache, continues on to internet server.
- wittr also requests some JavaScript. This opens a **web socket**, a persistent connection that continually streams newer posts from the server.

### 1.11. Quiz: Changing Connection Types

### 1.12. Quiz: Testing Lie Fi Mode

### 1.13. Introducing Service Worker

[Next lesson](offline-2-sw.md)

[(Back to top)](#top)