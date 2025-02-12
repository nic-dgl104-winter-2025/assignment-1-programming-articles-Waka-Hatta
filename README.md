[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/_Y4t8UXw)
# dgl104-programming-article-repo

# Code review practices



## Introduction

If you join an IT company in the future and work as a programmer, code reviews will be an unavoidable part of your job. No matter how well a program is written, it may contain hidden bugs or inefficient code. Code reviews are essential for identifying these issues and refining the code. In this article, we will focus on the following three key aspects of code reviews and provide concrete examples to illustrate each point.

### 1. Attitude toward code reviews
### 2. What to check in code reviews
### 3. Effectiveness of code reviews
<br>

## 1. Attitude toward code reviews
First, we will discuss the attitude that both the reviewer and the reviewee should adopt when approaching a code review. Both the reviewer and the reviewee need the right mindset. Specifically, the following attitudes are crucial for an effective review process:<br><br>

### The Code Reviewee
Don’t interpret criticism of the reviewer’s code as an implication that the reviewer is an incompetent programmer. Code reviews are an opportunity to share knowledge and make informed engineering decisions. But that can’t happen if the reviewee perceives the discussion as a personal attack(Lynch, 2017).
Also, Reviewers sometimes express their frustration in comments. While this is not an appropriate attitude for a reviewer, they are human and can become emotional. As a developer, you need to be prepared for this. Ask yourself, "What constructive point is the reviewer trying to convey to me?" and try to grasp their true intention. Once you understand their intent, it is important for you to take constructive action.(Google, n.d.).<br><br>

### The Code Reviewer
Never say “you”! Word your feedback in a way that minimizes the risk of raising your teammate’s defenses. Be clear that you’re critiquing the code, not the coder. When an coder sees “you” in a comment, it brings their focus away from the code and back to themselves. This increases the risk that they’ll take your criticism personally(Lynch, 2017).
Moreover, the reviewee may have deeper knowledge of programming than the reviewer. Reviewers should always keep this in mind and use respectful and polite language when giving feedback.
This becomes particularly challenging when conducting code reviews online rather than in person. In face-to-face discussions, tone of voice, facial expressions, and gestures can help convey respect for the other person. However, when writing comments, reviewers must rely solely on text to communicate their message.
For example, it is important to carefully phrase comments as follows:
<div style="border: 2px solid gray; padding: 10px;">
<span style="color:red">#Bad: </span> “Why did you use threads here when there’s obviously no benefit to be gained from concurrency?”
</div>
<br>
<div style="border: 2px solid gray; padding: 10px;">
<span style="color:blue">#Good: </span>“The concurrency model here is adding complexity to the system without any actual performance benefit that I can see. Because there’s no performance benefit, it’s best for this code to be single-threaded instead of using multiple threads.” 
</div>
(Google, n.d.)
<br><br>
Additionally, The key principle to remember is that there is always a "better" code, but there no such thing as a "perfect" code. Keeping this in mind is essential when participating in a code review. <br><br><br>

## 2. What to check in code reviews
Next, I would like to discuss what should be checked during a code review. Specifically, the following points should be reviewed:<br><br>

### Functionality
The primary requirement is that the code aligns with the functional requirements. It must be verified that the code does not behave differently from the design specifications. Additionally, if parallel programming is used, it is necessary to check for potential deadlocks or race conditions. These types of issues are often difficult to detect simply by running the code, so careful code review is essential to ensure that no such problems can occur(Google, n.d.).<br><br>

### Code readability
The code should be clean, well-organized, and easy to understand. Check that the logic flows naturally and that comments and documentation are used appropriately. It is also necessary to check that the same process is not being repeated and that magic numbers are not being used. Magic numbers are numbers written directly into the source code, such as in the following example, whose intent and meaning are only known to the writer. 

<div style="border: 2px solid gray; padding: 10px;">
<span style="color:red">#Bad: Magic number</span> : Constants are written directly<br>
&emsp;&emsp;def calculate_circle_area(radius):<br>
&emsp;&emsp;return radius * radius * 3.14159 <br>
</div><br>
<div style="border: 2px solid gray; padding: 10px;">
<span style="color:blue"># OK </span> The value of PI is defined outside the function and referenced outside the function.<br>
&emsp;&emsp;PI = 3.14159<br>
&emsp;&emsp;def calculate_circle_area(radius):<br>
&emsp;&emsp;return radius * radius * PI<br>
</div>
<br>
Also, complex algorithms should be broken down into clear, manageable functions with descriptive comments explaining their purpose(Clickup, 2024). Direct transliterations of code into English, for example, do nothing to improve understanding, because you should assume that your reader at least knows Java:<br>
Ex) <span style="color:red">Bad comments in code</span>: Direct transliterations of code into English(MIT, 2016)<br>
<div style="border: 2px solid gray; padding: 10px;">
while (n != 1) { // test whether n is 1 ( don’t write comments like this) <br>
&emsp;&emsp;++i;&emsp;&emsp;// increment i<br>
&emsp;&emsp;l.add(n);&emsp;&emsp;// add n to l <br>
}
</div><br>

### Coding style and Consistency
Verify that the code adheres to established coding standards and conventions, including proper indentation, spacing, and bracket placement. This consistency helps maintain a uniform codebase and makes it easier for developers to collaborate and review(Clickup, 2024).<br><br>

### Clear naming
Names are important—they should be descriptive and meaningful. Ensure that variables, functions, and classes have names that convey their purpose and functionality.<br>
For example :
<div style="border: 2px solid gray; padding: 10px;">
<span style="color:red"># NG </span> Class roles are unclear and meanings are ambiguous<br>

&emsp;&emsp;class Processor:<br>
&emsp;&emsp;class Sender:
</div>
<br>
<div style="border: 2px solid gray; padding: 10px;">
<span style="color:blue"># OK </span> Class roles are clear<br>

&emsp;&emsp;class PaymentProcessor:   # It is immediately clear that this is a class that processes payments.<br>
&emsp;&emsp;class EmailSender:             # It is clear that this is a class that has the functionality to send email.
</div><br>

It's important to use more descriptive names and follow the lexical naming conventions of your language so that your code can be clearly read on its own(MIT, 2016).<br><br>

### Performance and efficiency
Check for performance issues such as inefficient algorithms and memory leaks. Introduce necessary review loops and recursive functions to ensure they work efficiently and don't introduce unnecessary complexity and resource consumption(Clickup, 2024).<br>
For example, here is an example of inefficient memory usage due to a large number of string concatenations:<br>
<div style="border: 2px solid gray; padding: 10px;">
<span style="color:red">NG :</span><br> public class StringConcatenationExample {<br>
&emsp;&emsp;public static void main(String[] args) {<br>
&emsp;&emsp;&emsp;String result = "";<br>
&emsp;&emsp;&emsp;for (int i = 0; i < 10000; i++) {<br>
&emsp;&emsp;&emsp;&emsp;result += "data" + i;  // Inefficient string concatenation<br>
&emsp;&emsp;&emsp;}<br>
&emsp;&emsp;&emsp;System.out.println("Final string length: " + result.length());<br>
&emsp;&emsp;}<br>
}
</div><br>
<div style="border: 2px solid gray; padding: 10px;">
<span style="color:blue"> OK :</span> <br>public class StringBuilderExample {<br>
&emsp;&emsp;public static void main(String[] args) {<br>
&emsp;&emsp;&emsp;StringBuilder result = new StringBuilder();<br>
&emsp;&emsp;&emsp;for (int i = 0; i < 10000; i++) {<br>
&emsp;&emsp;&emsp;&emsp;result.append("data").append(i);  // Efficient string concatenation<br>
&emsp;&emsp;&emsp;}<br>
&emsp;&emsp;&emsp;System.out.println("Final string length: " + result.length());<br>
&emsp;&emsp;}<br>
}
</div><br>

### Error handling and logging
Error handling and logging are about having a plan for unexpected mishaps. Verify that the code includes robust error handling to manage potential issues gracefully and log important events for debugging purposes(Clickup, 2024). Also make sure the correct level of logging is emitted. Too much logging can cause critical logs to be missed. Having the right logs emitted at the right time and at the right level is important to maintain.
Examples of logging levels include(:

<b>
INFO: Significant and noteworthy business events.<br>
WARN: Abnormal situations that may indicate future problems.<br>
ERROR: Unrecoverable errors that affect a specific operation.<br>
FATAL: Unrecoverable errors that affect the entire program.<br>
</b></br></br>


## 3. Effectiveness of code reviews
So far, we have discussed the right mindset for code reviews and the key aspects to check during the process. But what exactly are the benefits of conducting a code review correctly?<br><br>

### Improved code accuracy
Code reviews make it possible to detect bugs that the original developer may not notice. Even if the developer believes they have written the code correctly, there may be discrepancies with the specifications or design, as well as careless mistakes. By having multiple people objectively review the source code, the risk of overlooking such bugs can be reduced. <br>
Another advantage of code reviews is the ability to optimize the source code. Even if there are no functional issues, unnecessary lines of code may exist—for example, a process that could be written in a single line is spread across multiple lines. Redundant code not only reduces readability but can also become a potential source of bugs in the future. A code review involving experienced developers can help identify such inefficiencies in the code. Optimizing the source code not only reduces the burden of maintenance but also helps mitigate the risk of potential bugs (QBOOK、2025).<br><br>

### Code reviews share knowledge
Code reviews also serve as a means for knowledge sharing and alignment within the development team. They provide an opportunity to inform team members about best practices, such as highlighting coding patterns that are prone to bugs.<br>
Many development teams and projects establish their own coding rules. However, it is not uncommon for these rules to be overlooked, leading to inconsistencies in coding styles among team members. By reinforcing these rules through code reviews, teams can standardize coding practices and maintain consistency across the project.(QBOOK, 2025)<br><br>

### Avoiding conflicts
By conducting code reviews, unnecessary conflicts during Git merges can be avoided. Without code reviews, developers may only notice conflicting or incorrect code when attempting to merge it into Git. Performing code reviews before merging helps reduce the wasted time to investigate and fix the causes of conflicts.<br><br>

### Contributes to the skill enhancement of development team members
Code reviews involving experienced developers will improve the skills of the development team. Knowledge will be accumulated through the comments made during code reviews, and coding skills will improve. Young engineers in particular need to be aware of their mistakes in order to grow. By receiving accurate comments, they will be able to realize that there is a better way to write something. Code reviews are also a place where senior engineers can give young engineers hints on how to grow(QBOOK, 2025).<br><br>


## Conclusion
As mentioned above, code reviews have a significant impact when developing a system as a team. Conducting code reviews improves code accuracy and reduces unnecessary conflicts during program merges.<br> Additionally, it facilitates knowledge sharing within the team and contributes to skill enhancement.<br> However, to make code reviews effective, both the reviewer and the reviewee must have a proper understanding of the process and the right mindset. Furthermore, reviewers need to provide appropriate checks and feedback during the review.<br>
In the future, when you become part of a system development team, I hope you will recall the contents of this article and find it useful.<br><br><br>
 


## References

ATLASSIAN. (n.d.). Why code reviews matter (and actually save time!)<br>
https://www.atlassian.com/agile/software-development/code-reviews?utm_source=chatgpt.com<br><br>

Better Stack. (2024, October 24). Logging Best Practices.12 Dos and Don'ts<br>
https://betterstack.com/community/guides/logging/logging-best-practices/<br><br>

Clickup. (2024, October 3). How to Create a Code Review Checklist.<br>
https://clickup.com/blog/code-review-checklist/<br><br>

Google. (n.d.). Google Engineering Practices Documentation. Handling pushback in code reviews. 
https://google.github.io/eng-practices/review/reviewer/pushback.html<br><br>

Lynch, M. (2017, October 12). How to Do Code Reviews Like a Human (Part One).<br> https://mtlynch.io/human-code-reviews-1/<br><br>

MIT. (2016, Spring). Reading 4: Code Review.<br>
https://ocw.mit.edu/ans7870/6/6.005/s16/classes/04-code-review/<br><br>

QBOOK. (2025, February 5). What is a code review?. Explaining 4 benefits and points to keep in mind.<br>
https://www.qbook.jp/column/1649.html<br><br>

