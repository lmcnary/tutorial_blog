---
title: "Getting Started With APIs in Python"
---

# What is an API?

An **API**, which stands for Application Programming Interface, is a set of rules that allows different software applications to communicate with each other. It's sort of like a messenger that takes your request, delivers it to another system, and brings back a response. Without APIs, a lot of what we do online would not be possible. For example:
- The weather app on your phone fetches weather data from an API instead of measuring it itself.
- Payment services like Paypal and Venmo use APIs so that online payments can be processed securely.
- Google Maps has an API that allows developers for other apps to embed maps, calculate routes, or estimate travel times.
APIs act as the bridge between applications, making it possible for them to share data and functionality in a consistent and structured way.

## Learning Outcomes

In this guide we will learn how to fetch data from a public API using Python’s requests library and print JSON responses. By the end of this tutorial, you will be able to: 

- Set up your environment
- Make API requests using Python's requests library
- Inspect and use the returned data

# How APIs work (crash course)
A majority of APIs used on the internet are based on **HTTP**, which is the same protocol your web browser uses. When you interact with an API, you typically send a **request** to its server. The server processes your request and sends back a **response**.

Within your request you can specify different things like:
- the **endpoint**: this is the url where the resources you want access to are located
- the **method**: this indicates what kind of action you want to perform. Popular methods include GET or POST (we will be focusing on GET requests in this tutorial)
- some API requests may require additional information like location or authentication tokens

The response you get back from the server will contain:
- a **status code**: this indicates whether your request was successful (200) or if there was an error (404 Not Found, 500, etc)
- the **data**: This is the information you requested typically formatted in JSON

understanding these components is crucial for effectively working with APIs.


## Set up Your Environment
To get started with interacting with an API using Python, you will need to set your environment. This includes installing Python and installing the requests library.

To make sure you have Python installed, you can check by running the following command in your terminal or command prompt:

```bash
python --version
```
If you don't have Python installed, you can download it from the official website: [python.org](https://www.python.org/downloads/).

Next, make sure you have the requests library installed. You can install it by running the following command:

```bash
pip install requests
```
Once installed, import it into your Python script

```python
import requests
```

## Making API Requests
To make a request to an API, you will need the API endpoint URL. This is the URL where the API is hosted and where you will send your requests. We will use a GET request to fetch data from the API.
In this example, we are sending a get request to an API and printing the JSON response 

```python
response = requests.get('https://my-json-server.typicode.com/typicode/demo/posts')
data = response.json()
print(data)
```
This request asks the API to return a list of posts. The response is then converted to JSON format and printed to the console. It will look like a Python dictionary and will contain fields such as "id" and "title".

## Inspecting and Using the Data
The API should return a JSON response that looks something like this:

```json
[
  {
    "id": 1,
    "title": "Post 1"
  },
  {
    "id": 2,
    "title": "Post 2"
  },
  {
    "id": 3,
    "title": "Post 3"
  }
]
```
Getting the data is just the first step. Once you have the response, you can inspect and use it in your application. You can treat it just like a Python dictionary or list. For example, you can loop through this list and access and print each ID and title like this:

```python
for post in data:
    print(f"Post ID: {post['id']}, Title: {post['title']}")
```
Output:
```
Post ID: 1, Title: Post 1
Post ID: 2, Title: Post 2  
Post ID: 3, Title: Post 3
```

In some of the more complex APIs, you may need to handle nested JSON arrays. For example:
```json
{
  "user": {
    "id": 1,
    "name": "John Doe",
    "posts": [
      {
        "id": 101,
        "title": "First Post"
      },
      {
        "id": 102,
        "title": "Second Post"
      }
    ]
  }
}
```
If we wanted to access the titles of John Doe's posts, we could do it like this:

```python
for post in user_data['user']['posts']:
    print(post['title'])
```
Understanding how to navigate nested data structures is one of the key skills when working with APIs.
## Handling Errors and Status Codes
When working with APIs, not every request will be successful. Maybe the endpoint is incorrect or the server is down. You can check the status code to see if your request was successful before working with the data.
```python
if response.status_code == 200:
    print("Request was successful!")
    # now you can begin working with the data
else:
    print(f"Error: {response.status_code}")
```
This kind of error handling will help you identify issues early and save time debugging later on.

## Conclusion
APIs are powerful tools that allow you to access and interact with data from all different kinds of services. By using Python's requests library, you can easily make API requests and work with the returned data.

Now it's your turn!
Your task is to:
1. Create a new Python script
2. Use the requests library to make a GET request to a public API of your choice (I challenge you to find one with nested data!)
3. Try checking the status code of your request
4. Print the JSON response to the console
5. Inspect the data and try to access specific fields inside the JSON response.
Experiment with different APIs and see what kinds of data you can work with.

