---
author: "Tyler Lyle"
date: 2018-12-13
linktitle: gatoreducator-contributions
title: GatorEducator Contributions
highlight: true
---

### What is GatorGrader?

GatorGrader is one of many subsidiary tools under the GatorEducator organization.  The GatorEducator organization stores many different education oriented tools developed by Computer Science students at Allegheny College, with GatorGrader being specifically geared towards the automatic grading of repositories.  GatorGrader is designed for use with GitHub, GitHub Classroom, Travis CI, and Gradle.  As such, GatorGrader has a design that allows the program to interface with these platforms, as well as meet required features for grading.

Overall, the GatorGrader system uses Gradle to build projects, with certain specifications preset in a `.yml` file that are verified during the Gradle build.  After the build process, GatorGrader outputs the results of the expected checks and verifies if these were indeed fulfilled by the student.  Potential ways to verify students' submitted work is to check for a minimum number of repository commits, check to verify a file exists, check for paragraph and word count, and check for a main method in source code.  Additional methods of verification are also possible, with new checks being implemented frequently.


### Contributions

My contributions to GatorGrader are primarily in the form of tackling issues in the GitHub issue tracker.  Specifically, I worked in a [team](https://github.com/orgs/GatorEducator/teams/cs481-team2) of 6 others on [issue 81](https://github.com/GatorEducator/gatorgrader/issues/81) and [issue 97](https://github.com/GatorEducator/gatorgrader/issues/97).  These issues typically required a plan that came in <IDK> steps.  The first step would require us to first  select an issue on the issue tracker and gather information on how to solve it.  After we selected an issue we felt we could collectively solve, the second step was to select a design and divide the task with each of us playing an equal part while working to our individual strengths.  And the third step requiring us to implement and test the solution.

Typically, this meant that initial activities were done in a team-oriented fashion.  An example of this is when first tackling issue 81.  This issue asked to consider the use of a Markdown parser to break markdown into a syntax tree.  However, our team received completed code and we were required to write test cases for this team to verify their work.  Thus, the first task for our team was to analyze `test_fragments.py` program and garner understanding of what the current solution was, and how it could be updated with the new code provided.  After the code was analyzed and our team had a mutual understanding of the task at hand, we all brainstormed ideas for what we need to test.  

The decided tests were in relation to paragraphs and word count, and more specifically what counted as words and what should and should not split the paragraph.  For example, lists should denote the end of a paragraph and text in a code block should also count towards word count.  On an individual level, I provided the test case code that verified that lists, both ordered an unordered, did terminate a paragraph.  Additionally, I wrote code to verify that list items do indeed contributed to word count.  Both of these were implemented within an existing framework that allowed method calls to be parameterized.  As a result, the tests were fairly straight forward to write, with a line containing a method call with some input values followed by the expected output values.

The next issue, issue 97, was a tad different in implementation with the planning process remaining the same.  Issue 97 had us add new sample repositories to the GatorEducator organization in order for new users to understand the different applications in which GatorGrader would be useful.  The issue also called for many different repositories to be created, such as repositories for C/C++, HTML and CSS, and R for Data Science.  Each repository would be unique as it would contain differing checks for the typical work expected for their related courses.  However, this issue was a tad different in that it also required additional help from potential users.

It was agreed upon from team communication that I would complete the R for Data Science and Python for Discrete Structures repositories.  This required me to meet with Professor Bonham-Carter in the Allegheny Computer Science Department.  When talking to Professor Bonham-Carter we agreed upon certain checks that should take place for use in grading these repositories. Professor Bonham-Carter also sent me two example repositories for aiding in understanding what the average lab repository would look like for these courses.  It was then my job to strip the repositories of any solution data, formulate and implement the checks for the repository, and ensure that it passed the GatorGrader build.



### Overall Learning

Overall, my learning experience was derived from learning to use industry grade software tools to complete these objectives.  However, additional experience was gathered from the solicitation of software requirements and team based activities.  This method of conducting course work was helpful in forcing me to act as a team and not just create new software my way, but inherit software I do not understand initially.  Thus, I had to first read the documentation/source code and set up an instance of GatorGrader on my computer to learn the design of the software.  Then I had to use this basic knowledge to select an issue as a part of a team, and implement a solution.  This forced me out of the "I did not build it" mindset that students often carry, and as a result, I had to look at the bigger picture of software, teams, requirement fulfillment, and most importantly time management.
