# Lab 2 worksheet

Use this file for the written notes in all five phases. The Canvas page gives the instructions. This is the only Markdown file you need to complete. You do not need to write paragraphs.

## What to do

Work through the five phases on the Canvas page:

1. Write one inference about what the system senses, infers and does.
2. Draw the interaction flow as a loop from the person's goal to system feedback.
3. Draw the normal interaction as a storyboard with as many moments as you need.
4. Show what happens when the inference is wrong and how the person recovers.
5. Choose one design check and draw an improvement into the storyboard.

Submit this worksheet with the three images you make for phases 2, 3 and 4.

## 1. Your interaction

Problem from Lab 1: People trying to obtain unconventional statement for a newly opened bank account struggle with receiving the appropriate documentation because the banking chatbot misinterprets requests for a “statement” as periodic bank statements, redirects users to unavailable resources, and prevents them from correcting the system’s assumption.

What should the system sense, infer and do?
The system senses the word "statement" in the users message AND how many times the user repeats a similar request after proferred solution
The system infers that "statement" means a periodic account statement the user can download from the mobile banking application.
The system replies with a short message on what it understood with evidence for it, and offers options: Yes, that’s it OR No, I need something else OR Talk to a person. If the user confirms, it links to the statements page.

When could that inference be wrong?
When the account has no statements yet OR When the user needs a different document, such as proof of account ownership and an account confirmation letter OR When the user repeats the request, which signals the first answer didn’t work OR When the system wrongly counts a link as a resolved task even with repeated similar request.
## 2. Your flow

Draw one image that joins these five parts into one interaction loop. Use one labelled box for each part and connect the boxes with arrows. After the feedback, connect the arrow back to the person's goal:

1. Person's goal: Obtain peculiar proof of ownership statement for a funding provider
2. What the system senses: Trigger words like "statement", repeat requests via chat history AND account status
3. What the system infers: Trigger word "statement" means user needs a periodic bank statement
4. What the system does and through which channel: Channel [In-app text chat with option buttos]. System (Conversational Agent- CA) provides evidence of inference and offers 3 paths: Yes, that’s it OR No, I need something else OR Talk to a person.
5. What feedback the person receives: Evidence of reasoning and path options

## 3. Your normal-interaction storyboard

Storyboard image: 02_storyboard_normal.png (5 frames)

Frame 1 - Goal and request: The user wants a document proving the account is theirs and asks for "a statement". The system picks up the word "statement" and checks the account.

Frame 2 - CA's reading: The CA says it has read this as a bank statement (the usual meaning) and lists four options. The user sees what the system assumed and has three buttons: Yes, that's it /Something else /Talk to a person.

Frame 3 - User corrects: The user taps "Something else". The system asks what the statement is for, with an open text box and no preset options, so an unusual request is not forced into a fixed list.

Frame 4 - Request submitted: The person describes the need in their own words. The system submits it as a special request, gives a wait time (2 working days, placeholder) and says where the document will appear.

Frame 5 - User decides: The CA asks whether it covered what the person needed. The person chooses Yes, all sorted / Not quite / Talk to a person. The system does not mark the task as done itself.

Design note: Ownership proof is deliberately not offered as a button in frame 2. If the system could have offered it, it would have done so at the first request. Asking an open question lets the person state an unusual need in their own words.

## 4. Your failure-and-recovery storyboard

Draw a second storyboard for this phase. This is the failure-and-recovery storyboard, not the Phase 2 flow. Use as many frames as you need to show the wrong inference, how the person notices, the recovery and what the system should learn. Include:

- What wrong inference does it make?
The CA incorrectly inferred that the user wanted a standard bank statement, despite account information indicating that no statements were available for the newly opened account.

- How does the person notice?
Finds no statement is proffered link

- How do they recover?
CA senses the repeat request

- What should the system learn?
A repeated request means task is not resolved or completed
A new account has no statements, so do not offer link despite users' choice
CA should clarify trigger words early on to prevent loop
After two repeats, connect user to a human representative

## 5. Check the storyboard with a secondary user

Look at your Phase 3 storyboard from the perspective of a secondary user, someone else who would use the system. Choose one question below, pick one frame and revise it so the interaction is clearer for that person:

- Is it apparent what the system can do?
- Is it apparent how well the system can do it?
- Is it apparent why the system acted?
- Can the person correct it?
- Can the person see the consequences of an action?

Show the revised frame in your storyboard. In the worksheet, write:

- Which question did you choose?
Can the person correct it?

- Which frame did you change?
Frame 2: The CA's reading and frame 4: the request result

- What was unclear?
For this person, the Phase 3 reading was 8 lines long, offered four options at once, used banking words such as "delivery" and "copies" and had small buttons. They may not realise they can disagree with the system, and correcting it meant typing a free-text answer.

- What did you change and why?
The reading is now 4 short lines in plain words with one question. Correcting the system is now one tap, with tappable options instead of typing. This lowers the effort of correcting the system.
## Save

Submit this worksheet, one flow image, one normal-interaction storyboard image and one failure-and-recovery storyboard image. Use placeholders instead of real names, faces or private messages.
