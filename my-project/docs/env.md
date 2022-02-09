So to begin setting up our environment, let's start by creating a project folder in a desired location that will hold the contents of our project. Name it `my-project`.

```
$ mkdir my-project
$ cd my-project
```

## Flutter
Now, to create a Flutter project, we first must fulfill the Flutter Requirements needed:

* Flutter SDK
* Chrome
* Optional: an IDE that supports Flutter. Visual Studio Code is used for this tutorial

Follow the [Building a Web Application with Flutter](https://docs.flutter.dev/get-started/web) tutorial to get your machine set up with the Flutter SDK.

**IMPORTANT NOTE**: The instructions provided by the Flutter Docs only sets your PATH variable for the current terminal window and not for future terminal windows. Follow [these](https://stackoverflow.com/questions/50652071/flutter-command-not-found) instructions to permanently add Flutter to your path. 

### Create a new Flutter project with web support

Run the following commands to get the latest version of Flutter

```
$ flutter channel stable
$ flutter upgrade
```

And create and run a new Flutter project within the my-project directory. I named my flutter project `tg_flutter`.

```
$ mkdir my-project
$ cd my-project
$ flutter create tg_flutter
$ cd tg_flutter
```

Serve your app from localhost in Chrome by running the following command from the main directory of the project, `tg_flutter`.

```
$ flutter run -d chrome
```

This launches the application using the development compiler in the Chrome browser.

## Middleware

Requirements

* Python

## Create Middleware Directory

In the `my-project` directory, create a new directory to hold the goods for the middleware.

```
$ mkdir middleware
$ cd middleware
```

Your `middleware` and `tg_flutter` directories should sit next to each other in the `my-project` directory.

### Python Virtual Environment

Create a virtual environment using venv and Python.

```
$ python3 -m venv venv
```

Activate the new virtual environment.

```
$ source venv/bin/activate
```

There should now be (venv) in front of your terminal after activating the virtual environment. 
### Install Packages


### FastAPI Setup

### Run the API

### Explore the Endpoints



We will learn how to connect to our TigerGraph solution in the [Middleware](middleware.md) section.

## TigerGraph Cloud



## The Data