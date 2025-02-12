[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/_Y4t8UXw)
# dgl104-programming-article-repo

# Code review practices



## Introduction

If you join an IT company in the future and work as a programmer, code reviews will be an unavoidable part of your job. No matter how well a program is written, it may contain hidden bugs or inefficient code. Code reviews are essential for identifying these issues and refining the code. In this article, we will focus on the following three key aspects of code reviews and provide concrete examples to illustrate each point.

### 1. Attitude toward code reviews
### 2. What to check in code reviews
### 3. Effectiveness of code reviews
<br>

### 1. Attitude toward code reviews
First, we will discuss the attitude that both the reviewer and the reviewee should adopt when approaching a code review. Both the reviewer and the reviewee need the right mindset. Specifically, the following attitudes are crucial for an effective review process:

#### ＜The Code Reviewee＞
Don’t interpret criticism of the reviewer’s code as an implication that the reviewer is an incompetent programmer. Code reviews are an opportunity to share knowledge and make informed engineering decisions. But that can’t happen if the reviewee perceives the discussion as a personal attack(Lynch, 2017).
Also, Reviewers sometimes express their frustration in comments. While this is not an appropriate attitude for a reviewer, they are human and can become emotional. As a developer, you need to be prepared for this. Ask yourself, "What constructive point is the reviewer trying to convey to me?" and try to grasp their true intention. Once you understand their intent, it is important for you to take constructive action.(Google, n.d.).

#### ＜The Code Reviewer＞
Never say “you”! Word your feedback in a way that minimizes the risk of raising your teammate’s defenses. Be clear that you’re critiquing the code, not the coder. When an coder sees “you” in a comment, it brings their focus away from the code and back to themselves. This increases the risk that they’ll take your criticism personally(Lynch, 2017).
Moreover, the reviewee may have deeper knowledge of programming than the reviewer. Reviewers should always keep this in mind and use respectful and polite language when giving feedback.
This becomes particularly challenging when conducting code reviews online rather than in person. In face-to-face discussions, tone of voice, facial expressions, and gestures can help convey respect for the other person. However, when writing comments, reviewers must rely solely on text to communicate their message.
For example, it is important to carefully phrase comments as follows:

<span style="color:red">#Bad: </span> “Why did you use threads here when there’s obviously no benefit to be gained from concurrency?”
<br><br>
<span style="color:blue">#Good: </span>“The concurrency model here is adding complexity to the system without any actual performance benefit that I can see. Because there’s no performance benefit, it’s best for this code to be single-threaded instead of using multiple threads.” 
(Google, n.d.)
<br><br>
Additionally, The key principle to remember is that there is always a "better" code, but there no such thing as a "perfect" code. Keeping this in mind is essential when participating in a code review. 
<br><br><br>
### 2. What to check in code reviews
Next, I would like to discuss what should be checked during a code review. Specifically, the following points should be reviewed:

<Functionality>
The primary requirement is that the code aligns with the functional requirements. It must be verified that the code does not behave differently from the design specifications. Additionally, if parallel programming is used, it is necessary to check for potential deadlocks or race conditions. These types of issues are often difficult to detect simply by running the code, so careful code review is essential to ensure that no such problems can occur(Google, n.d.).




<Code readability>
The code should be clean, well-organized, and easy to understand. Check that the logic flows naturally and that comments and documentation are used appropriately. It is also necessary to check that the same process is not being repeated and that magic numbers are not being used. Magic numbers are numbers written directly into the source code, such as in the following example, whose intent and meaning are only known to the writer. 
