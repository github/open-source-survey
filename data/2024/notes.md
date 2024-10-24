This document contains notes for working with the 2024 GitHub Open Source Survey dataset (which includes a subset of the 2017 GitHub Open Source Survey dataset).

## 1. Known data quality issues
 
From 2017:

> Due to an implementation error, a number of respondents who selected 'Rudeness or Hostility' on the NEGATIVE-WITNESS question were not able to select additional options, despite the question wording indicating multiple selections were permitted. This was corrected on 3/22/2017 at 11:45am EDT.
> 
> Some responses were submitted after the study period closed for that sample. These appear to be cases where respondents saved the link for completion at a later time.

For 2024: due to an implementation error, some questions that were intended to be conditional were not actually conditional. For example, the question "Which is closest to your employer's policy on using open source software applications?" was intended to be conditional on the respondent indicating that they were employed either full-time or part-time. However, the question was actually presented to all respondents. In the clean `survey_data.csv` file, we have filtered out responses to these questions where the respondent did not meet the intended condition.

See the `clean_data/README.md` file for more information about the data cleaning process.

## 2. Dates

`DATE.SUBMITTED`: records the timestamp of response submission in Eastern Daylight Time, NOT the local time of the respondent. 
 
## 3. Recoded data

Open ended responses have been recoded only in the cases where the frequency of a type of response indicated that the closed response options missed a common case, or where their wording was ambiguous.
  - MULT.LOCATION_OF_FIRST_COMPUTER_INTERNET: open ended responses that indicated a place of employment have been recoded into a new category labeled 'At work (recoded from open ended)'
  - MULT.FIND_HELPER and MULT.FIND_HELPEE: open ended responses that indicated public online spaces (e.g. IRC, chat, StackOverflow) were recoded into the category corresponding to asking/asked for help in a public forum. 

## 4. Language

The survey was presented in English by default.  The introductory text included directions to finding selecting an alternative language (Traditional Chinese, Japanese, Spanish, and Russian). Translations were obtained through a paid vendor, with validation and corrections from the open source community via the public project repository. Despite great contributions from the community; there may be discrepancies in the instrument between the English version and translations, particularly in the wording of response scales. 
  - `TRANSLATED` indicates whether a respondent completed the English version of the questionnaire (0) or one of the translations (1).
