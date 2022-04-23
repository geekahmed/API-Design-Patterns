This is my summary of the API design patterns, by JJ Geewax.
Contributions: Issues, comments and pull requests are super welcome 😃
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->
# Table of Contents
- [Table of Contents](#table-of-contents)
- [Chapter 1. Introduction to APIs](#chapter-1-Introduction-to-APIs)
- [Chapter 2. Introduction to API design patterns](#chapter-2-Introduction-to-API-design-patterns)
- [Chapter 3. Naming](#chapter-3-Naming)
- [Chapter 4. Resource scope and hierarchy](#chapter-4-Resource-scope-and-hierarchy)
- [Chapter 5. Data types and defaults](#chapter-5-Data-types-and-defaults)
- [Chapter 6. Resource identification](#chapter-6-Resource-identification)
- [Chapter 7. Standard methods](#chapter-7-Standard-methods)
- [Chapter 8. Partial updates and retrievals](#chapter-8-Partial-updates-and-retrievals)
- [Chapter 9. Custom methods](#chapter-9-Custom-methods)
- [Chapter 10. Long-running operations](#chapter-10-Long-running-operations)
- [Chapter 11. Rerunnable jobs](#chapter-11-Rerunnable-jobs)
- [Chapter 12. Singleton sub-resources](#chapter-12-Singleton-sub--resources)
- [Chapter 13. Cross references](#chapter-13-Cross-references)
- [Chapter 14. Association resources](#chapter-14-Association-resources)
- [Chapter 15. Association resources](#chapter-15-Add-and-remove-custom-methods)
- [Chapter 16. Polymorphism](#chapter-16-Polymorphism)
- [Chapter 21. Pagination](#chapter-21-Pagination)
<!-- /TOC -->

# Chapter 21. Pagination
## Summary
- Pagination allows large collections of results (or large single resources) to be consumed in a series of bite-sized chunks rather than as a single large API response using three special fields: maxPageSize , pageToken , and nextPageToken .
- If there are more pages, a response will include a nextPageToken value, which can be provided in the pageToken field of a subsequent request to get the next page.
- We rely on a maximum page size rather than an exact page size as we don’t know how long it will take to fill a page exactly and must reserve the ability to return even before a page of results is fully populated.
- Paging is complete when a response has no value for the next page token (not when the results field is empty).
## Exercises
- Why is it important to use a maximum page size rather than an exact page size?
- What should happen if the page size field is left blank on a request? What if it’s negative? What about zero? What about a gigantic number?
- How does a user know that pagination is complete?
- Is it reasonable for page tokens for some resource types to have different expirations than those from other resource types?
- Why is it important that page tokens are completely opaque to users? What’s a good mechanism to enforce this?
