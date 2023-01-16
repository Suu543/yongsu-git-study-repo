# Browsing History

contents:

1. Search for commits (by author, date, message, etc)
2. View a commit
3. Restore your project to an earlier point
4. Compare commits
5. View the history of a file
6. Find a bad commit that introduced a bug

## Starter

```txt
<!-- objectives.txt -->
OBJECTIVES

By the end of this course, you'll be able to
- Create snapshots
- Browse history
- Create and merge branches
- Collaborate with others
- Work with both the command line and visual tools
```

```txt
<!-- audience.txt  -->
AUDIENCE

This course is for anyone who wants to learn Git.
No prior experience is required.
```

```txt
<!-- toc.txt  -->
TABLE OF CONTENT

Creating Snapshots
  - Initializing a repository
  - Staging changes
```

```txt
<!-- sales-page.txt -->
```

```git
touch objectives.txt
// 상단의 objectives.txt 작성

git add objectives.txt
git commit -m "First: objectives text file for browsing history

// ----------------------------------------
touch audience.txt
// 상단의 audience.txt 작성

git add audience.txt
git commit -m "Second: audience text file for browsing history

// ----------------------------------------
touch toc.txt
// 상단의 toc.txt 작성

git add toc.txt
git commit -m "Third: toc text file for browsing history

// ----------------------------------------
sales-page.txt
// 상단의 sales-page.txt 작성

git add sales-page.txt
git commit -m "Fourth: sales-page text file for browsing history
```
