---
date: 2024-10-28
title: Survey D.X. Report
---
> Complete report: [[Survey Report - Azure Pipelines DX.pdf]].
> 
> For archival purposes the survey itself is here: [[Azure DevOps pipeline survey - Google Forms.pdf | Azure DevOps pipeline survey]].
## Executive Summary

The Azure Pipelines DX Survey Report, prepared for Info Support, explores developer frustrations with Azure Pipelines and identifies areas for improvement to enhance the developer experience. Given the challenges developers face, primarily the need to validate pipelines by running them, the survey aimed to pinpoint the most frequent issues and prioritize features for a proposed diagnostic tool.

### Objectives and Methodology

The survey, conducted among 29 Info Support developers, focused on identifying the most problematic features in Azure Pipelines, ranked by frequency, developer proficiency, and severity of issues. A weighted scoring model was applied to provide a ranking, ensuring an objective prioritization of issues.

### Key Findings

1. **Top Issues:** The most problematic features were compile-time expressions, stage-level variables, predefined variables, and template parameters.
2. **Error Messages:** Developers found Azure Pipelines’ error messages to be moderately helpful, often insufficient for quick troubleshooting.

### [[Survey Report - Azure Pipelines DX.pdf#page=12 |Recommendations]]

1. **Diagnostic Focus Areas:** High-priority diagnostics include compile-time expressions, variable scope, template parameters, and conditions at job and stage levels.
2. **Enhanced Error Messaging:** Improved clarity in error messages could aid developers in resolving issues faster.

### Conclusion

The proposed diagnostic tool, guided by these insights, can substantially reduce troubleshooting time and improve productivity by providing real-time, in-editor feedback on common Azure Pipeline issues.

## Follow-Up Interviews  
As part of the information-gathering process, several follow-up interviews were conducted with developers. These interviews revealed that most developers primarily use their own editors to produce pipelines, occasionally switching to the Azure DevOps in-browser editor for specific scenarios, such as troubleshooting or applying minor changes. The insights from these interviews were consistent with the survey findings and, therefore, were not included in the primary report, as they were conducted after its submission.

> For archival purposes the interviews can be found here:
> 	- [[Azure Pipelines survey follow-up-20241011_111947-Meeting Recording.mp4 |Survey follow-up 2024-10-11]]
> 	- [[Azure Pipelines survey follow-up-20241011_103220-Meeting Recording.mp4|Survey follow-up 2024-10-11]]
> 	- [[Azure Pipelines survey follow-up-20241014_100541-Meeting Recording.mp4|Survey follow-up 2024-10-11]]
> 	- [[Recording.m4a |Survey follow-up 2024-10-15]]