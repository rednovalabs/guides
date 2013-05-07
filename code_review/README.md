Code Reviews
==============================================================

#### DO
* Accept that many programming decisions are opinions. Discuss tradeoffs, which you prefer, and reach a resolution quickly.
* Ask questions rather than make demands. ("What do you think about naming this `perform_action`?")
* Avoid using terms that could be seen as referring to personal traits. ("dumb", "stupid") Assume everyone is attractive, intelligent, and well-meaning.
* Be explicit. Remember people don't always understand your intentions.
* Be humble. ("I'm not sure - let's look it up.")
* Avoid selective ownership of code. ("mine", "not mine", "yours")
* Ask for clarification. ("I didn't understand. Can you clarify?")
* Explain why the code exists. ("It's like that because of these reasons. Would it be more clear if I rename this class/file/method/variable?")
    * If clarification questions pop up during the review, they will *definitely* pop up in 6 months NOT during the review. Refactor code so that the clarification is in the code or a comment. Example:
        * (during code review)
            * *Jane*: Doesn't that duplicate the built-in `json_encode`? Why are you doing that yourself?
            * *Jim*: Well, the PHP `json_encode` method blows up when I pass in this specific object. I had to work around it by writing my own.
        * (6 months later)
            * *John*: What on earth? This completely duplicates `json_encode`. I'll just rewrite it to take advantage of the built-in method.
        * (in production)
            * **OH NOES** :flame:
* Be grateful for the reviewer's suggestions. ("Good call. I'll make that change.")
* Communicate which ideas you feel strongly about and those you don't.
* Identify ways to simplify the code while still solving the problem.
* Let the author make the final decision on alternative implementations, especially f discussions turn too philosophical or academic (which can be an indication that it doesn't matter).
* Offer alternative implementations, but assume the author already considered them. ("What do you think about using a custom validator here?")

#### Don't
* Use hyperbole or sarcasm. ("always", "never", "endlessly", "nothing")
* Take it personally. The review is of the code, not you.



### Per Project
http://codeinthehole.com/writing/pull-requests-and-other-good-practices-for-teams-using-github/

### As a team
From [11 Best Practices for Peer Code Review - SmartBear](http://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&ved=0CDkQFjAA&url=http%3A%2F%2Fsmartbear.com%2FSmartBear%2Fmedia%2Fpdfs%2FWP-CC-11-Best-Practices-of-Peer-Code-Review.pdf&ei=cl-JUZK8C5LqqAGsl4GoAQ&usg=AFQjCNE-Fr044F19hN_Fada7Cfhj6V5yQw):
> It’s easy to see defects as a bad thing – after all they are mistakes in the code – but fostering a negative attitude towards defects found can sour a whole team, not to mention sabotage the bug-finding process.
>> Managers must promote the viewpoint that defects are positive. After all, each one is an opportunity to improve the code, and the goal of the bug review process is to make the code as good as possible. Every defect found and fixed in peer review is a defect a customer never saw, another problem QA didn’t have to spend time tracking down.>> Teams should maintain the attitude that finding defects means the author and reviewer have successfully worked as a team to jointly improve the product. It’s not a case of “the author made a defect and the review found it.” It’s more like a very efficient form of pair-programming.
>> Reviews present opportunities for all developers to correct bad habits, learn new tricks and expand their capabilities. Developers can learn from their mistakes – but only if they know what their issues are. And if developers are afraid of the review process, the positive results disappear.
>> Especially if you’re a junior developer or are new to a team, defects found by others are a good sign that your more experienced peers are doing a good job in helping you become a better developer. You’ll progress far faster than if you were programming in a vacuum without detailed feedback.
> Managers must continue to foster the idea that **finding defects is good, not evil, and that defect density is not correlated with developer ability**. Remember to make sure it’s clear to the team that defects, particularly the number of defects introduced by a team member, shouldn’t be shunned and will never be used for performance evaluations.

From [Best Kept Secrets of Peer Code Review](http://smartbear.com/SmartBear/media/pdfs/best-kept-secrets-of-peer-code-review.pdf):

It's really easy to get hurt feelings from code reviews. Remember these points:

1. Difficult code has more defects
2. More time spent reviewing code brings up more defects
3. It's all about making better code - nothing is personal
4. The more defects we find, the better!
5. Authors and reviewers should be proud of any stretch of code where many defects were found and corrected - cause dayum, that be some fine code right thar