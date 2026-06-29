# Planning: TakeMeter — CMV Argument Classifier

## Community
r/changemyview is a subreddit where individuals post personal beliefs 
or opinions they acknowledge may be flawed, inviting others to 
challenge and potentially change their view. The community is entirely 
text-driven, producing a wide spectrum of post quality. From bare 
assertions to well-reasoned arguments backed by evidence. This makes 
it an ideal space to classify discourse quality, since the distinction 
between a weak claim and a structured argument is exactly what the 
community itself values and rewards.

## Labels

**Assertion:** A forceful claim on a belief, opinion, or statement 
on a topic with no correlated information.
- Example 1: "Men are generally hornier than women" — bold claim, 
no real evidence supporting it.
- Example 2: "Every organized religion is a cult, a scam, or satire"
— sweeping claim restated different ways, no evidence.

**Anecdote:** A belief or position supported solely by personal 
experience or stories, with no external evidence.
- Example 1: "Shaming people for not going to therapy is 
counterproductive" — driven almost entirely by the author's 
personal situation.
- Example 2: "Girl math encourages women to overspend" — driven 
entirely by watching her friends spend money, no data cited.

**Argument:** A position supported by external evidence, logical 
reasoning, or verifiable data, not just personal experience 
or assertion.
- Example 1: "The argument that healthcare isn't a human right 
undermines all human rights" — builds a logical chain comparing 
how all rights require labor to enforce.
- Example 2: "Blue states are getting screwed by a system designed 
to suppress their political power" — cites GDP percentages, 
electoral college mechanics, structural comparisons.

## Hard Edge Cases
A post that mixes personal experience and external evidence is the 
hardest case. Decision rule: if the external evidence could stand 
alone without the personal story, label it Argument. If the personal 
story is load-bearing — meaning remove it and the post collapses — 
label it Anecdote.

Additionally, posts with emotional language may feel like anecdotes 
but default to Assertion if no personal experience is actually cited.

## Data Collection Plan
- Source: r/changemyview public posts & r/unpopular
- Target: 200 examples, ~67 per label
- Method: manual copy-paste into CSV
- If a label is underrepresented after 150 examples, deliberately 
seek out posts that fit the underrepresented label before stopping 
at 200.

## Evaluation Metrics
Accuracy alone is not enough because the dataset could be imbalanced,
making a model that predicts one label constantly look deceptively 
good. I will also use:
- F1 score per class — measures balance between precision and recall
for each label
- Confusion matrix — shows exactly which labels are being confused 
and in which direction
- Per-class precision and recall — identifies whether the model is 
over or under-predicting specific labels

## Definition of Success
The classifier will be considered successful if it achieves at least 
70% overall accuracy and no single class F1 score falls below 0.60 
on the test set. This threshold means the model is meaningfully 
better than random chance (33%) and useful enough to assist 
annotation in a real community tool.

## AI Tool Plan

**Label stress-testing:** Give Claude the three label definitions 
and edge case rules, ask it to generate 8-10 boundary posts. If 
any are unclassifiable, tighten definitions before annotating.

**Annotation assistance:** 

**Failure analysis:** After evaluation, paste all misclassified 
examples into Claude and ask it to identify patterns. Verify every 
pattern manually by re-reading the examples before including it 
in the report.

## What I learned ## 
**Baseline Results (Groq llama-3.3-70b-versatile, zero-shot)**
- Overall accuracy: 67.7%
- Argument F1: 0.74
- Anecdote F1: 0.71  
- Assertion F1: 0.57
- Anecdote had perfect precision but low recall (0.56) — 
  the model was conservative, only calling something Anecdote 
  when very confident but missing half of the real examples.
- Assertion was weakest, likely due to overlap with Anecdote 
  in zero-shot.

**Preprocessing Data**
 I learned that my labels had more overlap than I expected,the Anecdote/Argument boundary 
 was hardest where personal reasoning and weak logical structure coexist,
 which is also where humans disagreed most during annotation
