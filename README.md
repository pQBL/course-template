# Repository for creating a QBL course on Torus

## Overview
This repo uses AI to let you generate questions for a Question Based Learning (QBL) course from a predefined course skill map. It then lets you edit the questions and upload them automatically to the [Torus](https://oli.cmu.edu/torus/) educational platform, all in the same repo!

This is done using [GitHub Actions](https://github.com/features/actions) in combination with the OpenAI [Chat Completions](https://platform.openai.com/docs/guides/gpt/chat-completions-api) API for generating qustions and [Selenium](https://www.selenium.dev/) for the Torus automation.

## Table of Contents
- [Setup](#setup)
  - [1. Fork template repository](#1-fork-template-repository)
  - [2. Update worfkflow permissions](#2-update-worfkflow-permissions)
  - [3. Set up necessary credentials](#3-set-up-necessary-credentials)
  - [4. Activate GitHub Actions](#4-activate-github-actions)
- [How to create a course](#how-to-create-a-course)
  - [1. Create a skill map](#1-create-a-skill-map)
  - [2. Generate pages with questions](#2-generate-pages-with-questions)
  - [3. Review the pages](#3-review-the-pages)
  - [4. Add the pages to Torus](#4-add-the-pages-to-torus)
- [Video setup tutorial](#video-setup-tutorial)
- [Video demo tutorial](#video-demo-tutorial)
- [YAML quick guide](#yaml-quick-guide)


## Setup

In order to use this repo some initial setup is required, which is described in the following guide. Note that this guide assumes that you already have the necessary credentials (OpenAI API key, GitHub token and Torus login). There is also a [setup tutorial video](#video-setup-tutorial) that may help to guide you through the process.

### 1. Fork template repository

To begin, you need to create a fork (personal copy) of this [template repository](https://github.com/pQBL/course-template). This is done by clicking the **Fork** button at the top right of the repo starting page:

> ![image](/imgs/fork.png)

Fill in the name of the repo and click **Create fork**. You will then be riderected to your newly forked repo.

> *The rest of this documentation assumes you are in the forked repo.*

### 2. Update workflow permissions

The workflow needs to create new branches for each generated page. This is not allowed by default, so you need to enable it. To do this, go to **Settings > Actions > General** and make sure your workflow permissions are set up like this:

> ![image](/imgs/permissions.png)

### 3. Set up necessary credentials

The workflow uses credentials stored as [GitHub secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets). These need to be added in order for the workflow to function properly. To do this, go to **Settings > Secrets and Variables > Actions** and click the button labeled **New repository secret**:

> ![image](/imgs/secrets.png)

Create the following GitHub secrets in your forked repository (make sure to name them exactly as below):

| **Name**                | **Description**                                                                                     |
|-------------------------|-----------------------------------------------------------------------------------------------------|
| `OPENAI_API_KEY_KTH`    | API key for OpenAI                                                                                  | 
| `BOTS_ACCESS_TOKEN`     | GitHub access token that has read access to the torusbot and qbl-bot-pipeline repositories          |
| `CURRICULUM_URL`        | URL to the curriculum page of your course on Torus                                                  |
| `USER_EMAIL`            | Email for torus account that has access to your course                                              |
| `USER_PASSWORD`         | Password for torus account that has access to your course                                           |


### 4. Activate GitHub Actions

To activate GitHub Actions, simply navigate to the **Actions** tab and click the green "Enable" button:

> ![image](/imgs/activate.png)

This should bring up a page that looks like this:

> ![image](/imgs/actions.png)

The setup is now done, and you are ready to create your course.

## How to create a course

After the proper [setup](#setup) has been completed, the course creation process can be broken down into the following steps:

1. Create a skill map
2. Generate pages with questions
3. Review the pages
4. Add the pages to Torus

The following section explains these steps in more detail.

### 1. Create a skill map

**To create the skill map, modify the template provided in the [skillmap.yaml](/skillmap.yaml) file to fit your course.**

The file is written in the [YAML](https://en.wikipedia.org/wiki/YAML) format (check out the [YAML quick guide](#yaml-quick-guide) for the most important info). You can add and remove units and pages as you like. Each page can have several skills.

When you have saved a correct version of the skill map, you are ready to start generating questions.

### 2. Generate pages with questions

**To generate the pages, run the `qbl bot pipeline` workflow under the "Actions" tab.**

The workflow is run by first selecting the `qbl bot pipeline` workflow in the left panel, then pressing the "Run workflow" dropdown menu to the right, and finally pressing the green "Run workflow" button.

This will begin generating new pull requests for each page in the skill map. Each skill takes about two minutes to generate with ten questions per skill (which is the default). 

The question format is multiple choice with three answer alternatives (A, B and C), where only a single answer is correct. Every alternative has tailored feedback informing the user if the answer was correct or incorrect, and why.

As soon as the first pull request shows up you can start reviewing (while the rest of the pages are being generated).

### 3. Review the pages

**To review a page, edit the corresponding pull request.**

This is done under "Files changed" in the pull request. When you are done editing, click "Commit changes" to save.

Optionally, you can assign additional people to review the questions.

When the review step is done, you are ready to add the page to Torus.

> *To regenerate a page, delete the automatically generated branch corresponding to the page. After that, run the action again.* 

### 4. Add the pages to Torus

**To add the page to Torus, merge the corresponding pull request.**

This will trigger the `torus deployment` workflow, which will create the page and add the questions. The page is done!

Repeat the steps for every page to generate the whole course.

## Video setup tutorial
*Coming soon.*

## Video demo tutorial
*Coming soon.*

## YAML quick guide

* Try to mimic the provided template in [skillmap.yaml](skillmap.yaml).
* YAML is case sensitive.
* YAML uses indentation to denote hierarchy. Make sure you indent correctly.
* YAML wants indentation using spaces, not tabs. However, you likely don't need to worry about that as your editor will probably convert tabs to spaces automatically.
* YAML uses colons to denote key-value pairs. Ex. `key1: value1`. If the value text contains a colon, you must put the value text in quotation marks. Ex. `key1: "See the following: value"`.
