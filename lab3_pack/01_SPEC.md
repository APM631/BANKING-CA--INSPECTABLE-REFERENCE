# 01_SPEC.md: use case and system path
Use Case: A person with a newly opened bank account asks the in-app CA for "a statement" when they actually need a proof-of-ownership document for a funding provider.

## User goal
The person wants a document that proves they own the account, to give to a funding provider. They do not want a periodic bank statement.

## System inputs
User provides typed request. For example, "I'd like to request a statement".
System checks chat history to see whether the person has made the same request before.
System checks account status to see whether the account has any statements available.

## Processing and technology
-Extract: the conversational agent (CA) detects the trigger word "statement" in the message. 
-Technology: keyword-based intent detection (simulated).
-Infer: the CA assumes "statement" means a periodic bank statement, the usual meaning.
-Look up: the CA checks the account status and the chat history for repeated requests. 
-Technology: account-status data (simulated).
-Respond: the CA says what it understood and offers three buttons: Yes, that's it / Something else / Talk to a person. 
-Technology: in-app text chat with buttons.
-Hand off: if user taps "Something else", the CA asks an open question and submits a special request. If they tap "Talk to a person", they are handed to a human representative. 
-Technology: special-request system and human handover (both simulated).

## Intended result and next action
The CA returns its reading of the request, with the reason, and three options. 
The user can confirm, correct it, or ask for a human at any point. If the need is unusual, such as an ownership letter, the CA submits a special request with a wait time. The CA then asks whether this covered what they needed, and the task is only marked complete when the user confirms.

## Fallback strategy
-Ambiguous request: the CA states its reading and asks the person to confirm or correct it.
-Wrong reading ("Something else"): the CA asks an open question with no preset options, so an unusual need is not forced into a fixed list.
-Repeated request: the CA treats it as a sign that the first answer did not help, drops the earlier action and asks why the person needs it.
-Still not resolved after two repeats: the CA connects the person to a human representative.

## System path or interaction diagram
Add a flowchart, use-case diagram or system architecture sketch showing the person, input, processing, data or model or tool, response and next action. Label anything that is implemented, simulated or still planned.

## Test A: standard input (Account 1: 3 years old, 36 statements available)
Input: I need my latest statement

What the system receives: CA receives
-Typed message: I need my latest statement
-Chat history: no exact earlier requests (repeat count=0)
-Account status: 3 years old, 36 statements available

What it does:
-Detects for trigger words and infers the usual meaning for trigger word. For example, trigger word is statement and inference is periodic bank statement
-Checks account: statements exist, so inference is reasonable (simulated kyword detection)
-Replies with its reading and three buttons.

Response and next action:
-CA: "I think you want a copy of your latest bank statement. Is that right?" Buttons: Yes, that's it / Something else / Talk to a person.
-User taps "Yes, that's it".
-CA returns a link to the latest statement (simulated statements service).
-CA asks: "Does this cover what you needed?" Buttons: Yes, all sorted! / Not quite / Talk to a person.
-User taps "Yes, all sorted!". Only now is the task marked complete.
-At every step the person could correct the CA or ask for a human.

## Test B: problem input (Account 2: 6 days old, 0 statements available)
Input: I'd like to request a statement. 
User actually needs a proof-of-ownership letter for a funding provider but does not say so. All system components are mocked (simulated).

What the system receives:
-Typed message: "I'd like to request a statement".
-Chat history: no earlier requests (repeat count = 0).
-Account status: 0 statements available.

What it does:
-Detects the trigger word "statement" and infers a periodic bank statement (simulated keyword detection).
-Looks up the account (0 statements) but still replies with its standard reading and buttons.
-Later, when the request is repeated, the repeat counter rises to 1 and the CA drops its earlier action and asks why.

Response and next action:
-CA: "I think you want a copy of your latest bank statement. Is that right?" Buttons: Yes, that's it / Something else / Talk to a person.
-User taps "Yes, that's it".
-CA: "Here are your statements" with an "Open statements" link.
-User opens it and finds: "None found".
-User types the same request again.
-CA: "I see you've made the same request again, so that did not help. What do you need the statement for?" with a free-text box and "Talk to a person".
-User types: "Proof-of-ownership letter for my funding provider, with this address. XYZ Rd, West Midlands, AB 1CD".
-CA: "Thanks, I've sent a special request with this chat attached, so you won't need to repeat yourself. If approved, expect it in 2 working days." (2 days is a placeholder.)
-CA asks "Does this cover what you needed?" and the person decides.
-Outcome: the person reaches the right route, but only after a dead-end link and a repeated request.

## Review and revision
Use the tests to identify an interaction or system problem. Note the evidence, then describe one interaction change and one technology or system change. Explain why the changes help and run Test B again.

1. Did the system make clear what it can and cannot do?
Evidence (Test B): the CA said "I think you want a copy of your latest bank statement" and offered "Yes, that's it". It never said that this account has no statements.
Problem: the CA implied it could provide something it could not.

2. Did it show what it understood or extracted from the input?
Evidence (Test A and Test B): the CA states its reading ("your latest bank statement"), so the person can see what it understood. But it does not say why it read "statement" that way or what it checked on the account.
Problem: my diagram says the CA "says what it read and why", but the test wording only gives the conclusion, not the reason.

3. Could the person correct a wrong extraction or decision?
Evidence (Test B): the "Something else" button was available, but the person tapped "Yes, that's it". Nothing in the message warned them the reading might be wrong, and they only found out after opening the link and seeing "None found".
Problem: correction was possible but nothing prompted the person to use it, so the error was found late.

4. Did it ask for missing information instead of guessing?
Evidence (Test B): the CA guessed a periodic bank statement and sent a link. It only asked "What do you need the statement for?" after the person repeated the request.
Problem: the CA guessed first and asked later, and the person had to repeat themselves to trigger the question.

5. Did it keep the person in control of the next action?**
Evidence (Test A): the CA asked "Does this cover what you needed?" and did not mark the task complete until the person confirmed. Evidence (Test B): before that point, the person was sent down a dead-end link first.
Problem: control was good at the end, but the person lost time in the middle of Test B.

6. Did it respond honestly when a model, tool or data source was unavailable?
Not used. Both tests had working (simulated) data, so I have no evidence for this question. The fallback for unavailable data is described in Phase 1 but was not tested.

## Problem chosen for Phase 4
The CA checks the account but does not use what it finds. It offers a statements link it should know is empty, and it does not tell the person why it made that guess. The person has to find and fix the error themselves. This problem is seen in questions 1,3 and 5.

### Phase 4: revision and retest

Interaction change: the CA's message now says why it cannot offer a statement and asks one clear question. Instead of "Yes, that's it / Something else / Talk to a person", the buttons are "Tell me what I need / Talk to a person". The person is told up front what the CA found and has a one-tap way to describe their real need.

System change: I added a validation step between the account lookup and the response. Before the CA offers a statements link, it checks whether the account data supports that option. If the account has 0 statements, the CA does not offer the link. The keyword detection technology stays the same, because it was not the cause of the problem. The account data was already available and was not being used.

Updated system path: keyword detection finds "statement" -> account lookup -> validation: does the account have statements? (new) -> if yes, offer the reading and the three buttons; if no, explain why and offer "Tell me what I need / Talk to a person". The rule for two repeated requests is unchanged.

## Test B (revised)
Input: "I'd like to request a statement" (Account 2: 6 days old, 0 statements). Same input as before. All system components are mocked (simulated).

What the system receives:
-Typed message: "I'd like to request a statement".
-Chat history: no earlier requests (repeat count = 0).
-Account status: 0 statements, account 6 days old.

What it does:
-Detects the trigger word "statement" and infers a periodic bank statement (simulated keyword detection).
-Looks up the account and runs the new validation step: the account has no statements, so the CA does not offer a statements link (simulated).

Response and next action:
-CA: "I read 'statement' as a bank statement, the usual meaning. But your account is only 6 days old and has no statements yet, so I can't show you one. Is there something else you need?" Buttons: Tell me what I need / Talk to a person.
-User taps "Tell me what I need".
-CA: "No problem. What would you like to use the document for?" with a free-text box.
-User types: "Proof-of-ownership letter for my funding provider, with this address. XYZ Rd, West Midlands, AB 1CD".
-CA: "Thanks. This is a special request, not a standard statement. If approved, expect it in 2 working days." (2 days is a placeholder.)
-CA asks "Does this cover what you needed?" and the task is only marked complete when the person confirms.

## What was revised
-Before: the CA offered a statements link it should have known was empty. 
-After: it checks first and does not offer it.

-Before: the person found the problem themselves ("None found"). 
-After: the CA tells them why up front.

-Before: the person had to repeat the request to get the open question (4 actions: tap Yes, open link, retype request, type need). -After: they get it straight away (2 actions: tap "Tell me what I need", type need).

## Why the changes improve the interaction and system path
The CA now tells the person what it understood and why it cannot help, so they don't have to find a dead end and repeat themselves to get the question that matters. Using account data the system already had, stops it from offering something it knows will fail. The  is still in control, because they choose the next step and only they mark the task complete.