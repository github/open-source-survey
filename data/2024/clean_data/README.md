# Data cleaning

This file contains documentation for the data cleaning process used to produce the clean `survey_data.csv` and `negative_incidents.csv` files located in this directory.

## Goal

Our goal is to enable users to analyze the counts and proportions of survey responses across years.

## Question and choice text mappings

In order to compare data across years, users must be able to identify which questions from the 2024 survey correspond to which questions from the 2017 survey, and similarly, which choices from the 2024 survey correspond to which choices in the 2017 survey. While many survey questions and choices are consistent across years, some have changed (in minor ways, such as in punctuation, capitalization, and spelling corrections) between years. We have mapped the questions and choices across years in the following files:

- [`choice_text.csv`](../mappings/choice_text.csv)
- [`question_text.csv`](../mappings/question_text.csv)

After matching each question and choice in the 2024 survey to the corresponding question and choice in the 2017 survey, the 2017 and 2024 data were merged, with the choice and response text from the 2024 survey replacing the choice and response text from the 2017 survey, unless the choice or response text was missing in the 2024 survey, in which case the choice or response text from the 2017 survey was retained.

## `NULL` values for [one-hot encoded](https://wikipedia.org/wiki/One-hot) columns

In our [release of the 2017 survey data](https://github.com/github/open-source-survey/releases/tag/v1.0), we provided `.ANY` columns for one-hot encoded responses to indicate that the respondent selected at least one of the choices for that question, since a response of all zeroes is indistinguishable from a response where the respondent skipped the question.

This time, to make the data wrangling process a bit easier, we have replaced values where the respondent selected all zeroes with `NULL` values. As a result, users no longer have to adjust the response counts after the fact to account for respondents who did not select any values (e.g., see cell 171 in https://github.com/staeiou/github-survey-analysis/blob/master/github-survey-descriptive-stats.ipynb).

## Responses filtered for certain conditional questions

Due to an implementation error, some questions that were intended to be conditional were not actually conditional. For example, the question "Which is closest to your employer's policy on using open source software applications?" was intended to be conditional on the respondent indicating that they were employed either full-time or part-time. However, the question was actually presented to all respondents. In the clean `survey_data.csv` file, we have filtered out responses to these questions where the respondent did not meet the intended condition.
