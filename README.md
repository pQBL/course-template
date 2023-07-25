# Repository for creating a QBL course on Torus

## Overview
This repo uses AI to let you generate questions for a Question Based Learning (QBL) course from a predefined course skill map. It then lets you edit the questions and upload them automatically to the [Torus](https://oli.cmu.edu/torus/) educational platform, all in one workflow!

This is done using the OpenAI [Chat Completions API](https://platform.openai.com/docs/guides/gpt/chat-completions-api) for generating qustions and [Selenium](https://www.selenium.dev/) for the Torus automation.

## Table of Contents
- [Setup](#setup)
- [How to create a course](#how-to-create-a-course)
  - [1. Creating a skill map](#1-creating-a-skill-map)
  - [2. Generating pages with questions](#2-generating-pages-with-questions)
  - [3. Reviewing the pages](#3-reviewing-the-pages)
  - [4. Adding the pages to Torus](#4-adding-the-pages-to-torus)
- [Video set up tutorial](#video-set-up-tutorial)
- [Video demo tutorial](#video-demo-tutorial)
- [YAML quick guide](#yaml-quick-guide)

## Setup

To set up the workflow you need to do the below steps. The video tutorials further down will guide you through the process.

1. Create a fork of this template repository.

2. Set up five GitHub secrets. You need to create 5 GitHub secrets in your forked repository. Create the following secrets:

    1. OPENAI_API_KEY_KTH - API key for OpenAI
    2. BOTS_ACCESS_TOKEN - GitHub access token that has read access to the torusbot and qbl-bot-pipeline repositories
    3. CURRICULUM_URL - URL to the curriculum page of your course on Torus
    4. USER_EMAIL - Email for torus account that has access to your course
    5. USER_PASSWORD - Password for torus account that has access to your course

## How to create a course

After the proper [setup](/skillmap.yaml) has been completed, the course creation process can be broken down into the following steps:

1. Creating a skill map
2. Generating pages with questions
3. Reviewing the pages
4. Adding the pages to Torus

The following section explains these steps in more detail.

### 1. Creating a skill map

**To create the skill map, modify the template provided in the [skillmap.yaml](/skillmap.yaml) file to fit your course.**

The file is written in the [YAML](https://en.wikipedia.org/wiki/YAML) format (check out the [YAML quick guide](#yaml-quick-guide) for the most important info). You can add and remove units and pages as you like. Each page can have several skills.

When you have saved a correct version of the skill map, you are ready to start generating questions.

### 2. Generating pages with questions

**To generate the pages, run the `qbl bot pipeline` workflow under the "Actions" tab.**

The workflow is run by first selecting the `qbl bot pipeline` workflow in the left panel, then pressing the "Run workflow" dropdown menu to the right, and finally pressing the green "Run workflow" button.

This will begin generating new pull requests for each page in the skill map. Each skill takes about two minutes to generate with ten questions per skill (which is the default). 

The question format is multiple choice with three answer alternatives (A, B and C), where only a single answer is correct. Every alternative has tailored feedback informing the user if the answer was correct or incorrect, and why.

As soon as the first pull request shows up you can start reviewing (while the rest of the pages are being generated).

### 3. Reviewing the pages

**To review a page, edit the corresponding pull request.**

This is done under "Files changed" in the pull request. When you are done editing, click "Commit changes" to save.

Optionally, you can assign additional people to review the questions.

When the review step is done, you are ready to add the page to Torus.

> *For multiple uses, the branch corresponding to each pull request needs to be deleted.* 

### 4. Adding the pages to Torus

**To add the page to Torus, merge the corresponding pull request.**

This will trigger the `torus deployment` workflow, which will create the page and add the questions. The page is done!

Repeat the steps for every page to generate the whole course.

## Video set up tutorial
*Coming soon.*

## Video demo tutorial
*Coming soon.*

## YAML quick guide

1. Try to mimic the provided template in [skillmap.yaml](skillmap.yaml).
2. YAML is case sensitive.
3. YAML uses indentation to denote hierarchy. Make sure you indent correctly.
4. YAML wants indentation using spaces, not tabs. However, you likely don't need to worry about that as your editor will probably convert tabs to spaces automatically.
5. YAML uses colons to denote key-value pairs. Ex. `key1: value1`. If the value text contains a colon, you must put the value text in quotation marks. Ex. `key1: "See the following: value"`.
