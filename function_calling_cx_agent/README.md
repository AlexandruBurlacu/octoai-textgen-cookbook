# Customer service example for function calling and JSON-mode 

This repository contains the necessary code to run the OctoAI function calling with a DIY solution for converting product reviews to JSON payloads for Jira and interacting with the customer that posted the review. If you want to dive into more details about OctoAI's function calling capabilities, check out [this blog post](...).

If you would like to try this out, go to [octo.ai](https://identity.octoml.ai/oauth/account/sign-up) to create an account, generate your `OCTOAI_API_TOKEN`, and complete the guide.

## Setup

Before running anything, please first install the necessary dependencies with `poetry install` and make sure to specify your `OCTOAI_TOKEN` in the `.env` file.

## Dataset

The dataset used in this repository is [Amazon Reviews 2023](https://huggingface.co/datasets/McAuley-Lab/Amazon-Reviews-2023) from McAuley Lab. We specifically use `raw_meta_Magazine_Subscriptions` subsample for product descriptions and the `raw_review_Magazine_Subscriptions` subsample for corresponding product reviews.


## Running the demo

See `agent.py` file. It will read the specified number of product descriptions, find the corresponding reviews, parse and group them by topic, and depending on the review it may thank the customer, ask for clarifications, or apologize and create a Jira ticket. The Jira REST API call is mocked, but the payload is valid.

Both scripts require most of the same parameters, provided via environment variables.

- `NUM_PRODUCTS`: number of products to process. This is not the number of unique reviews, but only of unique products. By default it's 5.
- `FUNCTION_MODEL_NAME`: should be one of the OctoAI models that supports function calling. Currently these models are: `meta-llama-3.1-8b-instruct`, `meta-llama-3.1-70b-instruct`, and `meta-llama-3.1-405b-instruct`. The default value is `meta-llama-3.1-8b-instruct`.


Here's an example how to run `agent.py` using the newest Meta Llama 3.1 70b parameter model and process the reviews from 10 products.

```bash
FUNCTION_MODEL_NAME=meta-llama-3.1-70b-instruct NUM_PRODUCTS=10 poetry run python -m function_calling_cx_agent.agent
```
