# Repository for creating a QBL course on Torus

QBL ad

Why this repo?
- Torus
- Creating QBL questions
- Adding questions to torus website
- Workflow for AI assissted course material creation

Describe general workflow
- Review files, commit changes + request reviewers
- PR:s
- Delete branches

## Setup

To set up the workflow you need to do the below steps. The video tutorials further down will guide you through the process.

1. Create a fork of this template repository.

2. Set up five GitHub secrets. You need to create 5 GitHub secrets in your forked repository. Create the following secrets:

    1. OPENAI_API_KEY_KTH - API key for OpenAI
    2. BOTS_ACCESS_TOKEN - GitHub access token that has read access to the torusbot and qbl-bot-pipeline repositories
    3. CURRICULUM_URL - URL to the curriculum page of your course on Torus
    4. USER_EMAIL - Email for torus account that has access to your course
    5. USER_PASSWORD - Password for torus account that has access to your course

3. Update [skillmap.yaml](skillmap.yaml) the reflect how your course should be structured. Try to mimic the provided template.

    Quick YAML guide:

    1. Try to mimic the provided template in [skillmap.yaml](skillmap.yaml).
    2. YAML is case sensitive.
    3. YAML uses indentation to denote hierarchy. Make sure you indent correctly.
    4. YAML wants indentation using spaces, not tabs. However, you likely don't need to worry about that as your editor will probably convert tabs to spaces automatically.
    5. YAML uses colons to denote key-value pairs. Ex. `key1: value1`. If the value text contains a colon, you must put the value text in quotation marks. Ex. `key1: "See the following: value"`.

4. On the GitHub page for your forked repository:
    1. Click the actions tab
    2. Select the `qbl bot pipeline` workflow
    3. Use the `Run workflow` button to run the workflow

Congratulations! A bot is now busy helping you create course material. Pull requests (PR) will incrementally appear in your repository as the workflow progresses. You can start working on a PR as soon as it appears. The time to create a PR depends on the number of listed skills for that page. It takes roughly 2 minutes per listed skill.

Video set up tutorial

Video demo tutorial

Practical tips