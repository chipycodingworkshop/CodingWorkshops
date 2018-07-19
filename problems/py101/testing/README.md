**Introduction to PyTest and Continuous Integration**

[![Build Status](https://travis-ci.org/chipycodingworkshop/CodingWorkshops.svg?branch=develop%2Fci)](https://travis-ci.org/chipycodingworkshop/CodingWorkshops)

Objective:

- Introduction to unit testing with pytest
- How to setup continuous integration with Github and Travis-CI

<!-- TOC -->

- [1. Setup Instructions](#1-setup-instructions)
    - [1.1. Git and Github](#11-git-and-github)
    - [1.2. Travis setup](#12-travis-setup)
    - [1.3. Python](#13-python)
- [2. Quick Git command refresher](#2-quick-git-command-refresher)
- [3. Exercise 0: Project Setup](#3-exercise-0-project-setup)
    - [3.1. `team_organizer.py`](#31-team_organizerpy)
    - [3.2. `test_team_organizer.py`](#32-test_team_organizerpy)
    - [3.3. `Makefile`](#33-makefile)
    - [3.4. `Pipfile` and `Pipfile.lock`](#34-pipfile-and-pipfilelock)
    - [3.5. `pytest.ini`](#35-pytestini)
    - [3.6. `travis.yml`](#36-travisyml)
- [4. Exercise 1: Build](#4-exercise-1-build)
- [5. Exercise 2: Run the program](#5-exercise-2-run-the-program)
- [6. Exercise 3: Running the tests](#6-exercise-3-running-the-tests)
- [7. Execrise 4: Coverage](#7-execrise-4-coverage)
- [8. Exercise 6: Fail, Fix, Pass](#8-exercise-6-fail-fix-pass)
- [9. Exercise 7: Fixtures](#9-exercise-7-fixtures)
- [10. Exercise 8: Implement the tests that are empty](#10-exercise-8-implement-the-tests-that-are-empty)
- [11. Exercise 9: Implement the tests first, then the feature](#11-exercise-9-implement-the-tests-first-then-the-feature)
- [12. todo](#12-todo)

<!-- /TOC -->

# 1. Setup Instructions

## 1.1. Git and Github

After completing the above steps you should have a github account and be able to push
your local changes to this repository to github.

- Follow the setup steps described [here](https://help.github.com/articles/set-up-git/).
- Follow the steps described in [fork a repo](https://help.github.com/articles/fork-a-repo).
- Now fork [this repository](https://github.com/chicagopython/CodingWorkshops) by clicking the fork button.

## 1.2. Travis setup

In this section we will set up a Continuous Integration pipeline
with Travis-ci.

- First, head over to [Travis-CI.org](https://travis-ci.org/.)
- Sign in with your Github account, and accept the terms and conditions.
- On success, you should be at your profile page that lists the CodingWorkshop repository.
- Once you have located the repo, toggle the button next to the repository to enable pipeline travis CI

If you have multiple repositories, you will have to search for the repository.

## 1.3. Python

This project has made no attempt to be compatible with Python 2.7. 😎

Recommended version: Python 3.6

# 2. Quick Git command refresher

Below are the few most used git commands

    git checkout develop/ci      # checkout to develop/ci branch
    git checkout -b feature/cool # crate a new branch feature/cool
    git add -u                   # stage all the updates for commit
    git commit -am "Adding changes and commiting with a comment"
    git push origin develop/ci   # push commits to develop/ci branch

# 3. Exercise 0: Project Setup

By this step you should have the forked version of CodingWorkshop
repository in your machine. Lets take the time to look at the structure of this
project. All code is located under `/problems/py101/testing` directory.
Make sure you are in this directory for the remainder of this project.

Run `pwd` (`cwd` for Windows) on the command prompt to find out which directory you
are on.

Your output should end in `problems/py101/testing` and contain the files described
below.

## 3.1. `team_organizer.py`

This file is a simplified implementation of the problem of grouping the project
night attendees into teams of four based on the number of lines of code they have
written such that two team members have more lines of code than the other.

## 3.2. `test_team_organizer.py`

This file is the test for the above module written using Pytest.
These are the only two files that we will be making modifications to for this project.

## 3.3. `Makefile`

This file commands that are required building the project.

## 3.4. `Pipfile` and `Pipfile.lock`

These two files are used by `pipenv` to create a virtual enviornment that
isolates all the dependencies of this project from other python projects in your computer.
Learn more about [pipenv](https://docs.pipenv.org/).

## 3.5. `pytest.ini`

This file contains the configuration for `pytest`.

## 3.6. `travis.yml`

In addition to all the files in this directory, located at the root of the repository,
is a file called `.travis.yml`. This is used by the continuous intergration tool travis-ci.
This contains the information on how to build this python project.

# 4. Exercise 1: Build

From the `/problems/py101/testing` directory, run

    make

- Which are packages get installed?
- Which version of python is getting used?
- How many tests pass, skipped and how long did it take?
- Note a new directory `htmlcov` was created. We will revisit this in Exericse 5.
- What is difference in output when you run the `make` command again?

# 5. Exercise 2: Run the program

Start by running

    python team_organizer.py

This will drop you to the program's interactive prompt.
Below is a sample interaction where users named a, b, c,
d, e and f are added using the add command.
Following that, we run the `print` command where the users
are grouped in to max of size four where two users have
written less lines of code than the others.

    ```
    t (master *) testing $ python team_organizer.py
    Welcome to Chicago Python Project Night Team Organizer
    org> help
    help
    
    Documented commands (type help <topic>):
    ========================================
    add  help  print
    
    Undocumented commands:
    ======================
    exit
    
    org> help add
    help add
    Adds a new user. Needs Name slackhandle number_of_lines separated by space
    org> add a @a 100
    add a @a 100
    org> add b @b 200
    add b @b 200
    org> add c @c 300
    add c @c 300
    org> add d @d 400
    add d @d 400
    org> add e @e 500
    add e @e 500
    org> add f @f 50
    add f @f 50
    org> print
    print
    ['f, a, e, d']
    b, c
    org>
    ```

# 6. Exercise 3: Running the tests

Run

    make test

This will run the tests in the `test_team_organizer.py` file.

Run

    pipenv run pytest --help

Now check the flags that are present in the `pytest.ini` file against
the output of the `--help` command to see what each one does.

# 7. Execrise 4: Coverage

When we first ran `make`, `pytest` created a directory called `htmlcov`
that show you the coverage information about `team_organizr,py` code.
Open the `index.html` file inside `htmlcov` to check the lines that
has not be covered.

What is the % coverage of the code at this point?

# 8. Exercise 6: Fail, Fix, Pass

After setup is complete, next go back to the terminal and ensure that
you are on the develop/ci branch.

    git branch

should show an asterix next to `develop/ci` branch name.

You are now all set to fix the tests. Goto `test_team_organizer.py` and
find `test_add_a_person_with_lower_than_median` test. Notice this test is
skipped when run with pytest. To fix it remove the decorator `pytest.mark.skip`
and run `pytest` again. Commit the code and push it.

    git commit -am "Commit a failed test"
    git push origin develop/ci

Next, fix the test so that when you run `make test` again all the tests pass.
Go to travis-ci.org and inspect the output before and after fixing the test.
What is the coveraga value at this point?

# 9. Exercise 7: Fixtures

What are the two fixtures used in the tests and how are they different?

# 10. Exercise 8: Implement the tests that are empty

- test_add_a_person_who_has_never_written_code_before
- test_add_two_person_with_same_name_but_different_slack_handles

# 11. Exercise 9: Implement the tests first, then the feature

For the following two tests, first implement the test that defines
behavior. If you run the tests at this point, they should fail.
Then go back to `team_organizer` and implement the feature by changing
the code. If you think your implementation is complete, run `make test`.

- test_add_a_person_who_supplied_negative_lines_of_code
- test_add_same_person_twice

# 12. todo