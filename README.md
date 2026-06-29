                            *** # ai201-project3-takemeter  ****

# TakeMeter — CMV Argument Classifier
A fine-tuned text classifier built for CodePath AI201. The model classifies r/changemyview posts by argument structure labeled -> Assertion, Anecdote, or Argument.
Using manually annotated dataset of 200 examples from reddit. 
Built with DistilBERT and evaluated against a zero-shot Groq baseline
---

## Community Choice

## Community
r/changemyview is a subreddit where individuals post personal beliefs 
or opinions they acknowledge may be flawed, inviting others to 
challenge and potentially change their view. The community is entirely 
text-driven, producing a wide spectrum of post quality. From bare 
assertions to well-reasoned arguments backed by evidence. This makes 
it an ideal space to classify discourse quality, since the distinction 
between a weak claim and a structured argument is exactly what the 
community itself values and rewards.

---

## Label Taxonomy

**Assertion:** Assertion: A forceful claim on a belief or opinion with no supporting evidence, logical reasoning, or personal experience the position is stated as fact without any attempt to justify it.]
- Example 1: "Salt doesn't belong on chocolate.The salted chocolate trend is a bummer. Yes, good chocolate can have a small, imperceptible amount of salt, and baked desserts like cakes and cookies require it, but the chunks of salt on top of chocolate chip cookies, brownies, or chocolate bars is too much. It makes a sweet treat into a meh "snack". Entire cases of desserts are covered in salt now. We've lost our way."
  
- Example 2: "I’m gonna be honest, never dying would kinda rockI get the idea: everybody you knew is dead, your job is obsolete, yadda yadda But like, if you lived forever, there are SO MANY jobs you could have. You could be an accountant, a roughneck, a framer, a nurse, engineer, surgeon, whatever: and the whole time you would be getting perspective on other people’s lives without living the shitty part and watching them die.Honestly, not the worst thing in the world."

**Anecdote:** A belief or position supported solely by personal 
experience or stories, with no external evidence.

- Example 1: "Public Libraries are better than any streaming servicesI started to cancel my streaming subscriptions one by one, with just Netflix remaining and Peacock.All of them have the same problem, they don't have what I want to watch or worse, the things I enjoyed were moved out to another competitor. And at one time I was paying like 70 a monthNow enter my Public Library, has all the movies and shows on either physical media or through Hoopla (library streaming app thing) when I want them FOR FREE! I remember I wanted to watch some horror films for Halloween season, most of the titles were unavailable on any streaming platform whereas my library had them all on bluray and DVDPublic Library >> Streaming apps."
  
- Example 2: "Full-time in-person is genuinely better for most people and most companies.Don’t get me wrong, no commute and working from home in comfy clothes is not a bad thing, but after a few years of this experiment, I miss the energy of actually being around people. Quick conversations, seeing how others solve problems, and random brainstorming sessions just hit different on a zoom call.Gen Z especially is getting screwed remotely. You learn way more by watching and overhearing things in person than through scheduled calls and Slack pings.Culture feels fake online too. Everyone’s a little more guarded, and real friendships are harder to build. Plus a lot of people I know feel more isolated and “always on” than they did at the office. Change my mind."

**Argument:** A position supported by external evidence, logical 
reasoning, or verifiable data, not just personal experience 
or assertion.

- Example 1: "Farting in the presence of your loved ones isn't a flex people think it isI've seen people being very loud and proud about feeling free to fart in front of someone, be that their friends or spouses or whoever. They usually defend this "achievement" by saying that it means some deep level of trusting each other, being comfortable around each other, feeling safe to be the their authentic selves.And yes, while it does require some level of comfort, my opinion is that it's not something to be proud of.Firstly because there are other ways to show trust, comfort and feeling safe. There are other ways for your strong bond to manifest. Idk, allow yourself to cry, be emotionally intimate, entrust them with your secrets, etc. These are bigger, more meaningful signs of trust and comfort. The ones that really matter.And secondly, even if y'all are that comfortable, it's still a dick move to subject your loved ones to the stench. Wouldn't you want them to have the least amount of unpleasant experiences possible? If there is someone in the whole world who should care about their life being pleasant, shouldn't it be you? You don't go smearing shit on their pillows, it's nasty and unpleasant."
  
- Example 2: "Fades are the ugliest haircut and its become an epidemic at this pointI'm gonna say it. The fade haircut looks terrible on like 90% of people who get one and I'm tired of pretending otherwise.Every single guy under 35 has the exact same haircut now. Skin fade on the sides, slightly longer on top, maybe some texture if they're feeling wild. Walk into any barber shop and it's just an assembly line of dudes getting the exact same cut. Go to a bar on a friday night and it looks like everyone spawned from the same character creation screen.The worst part is it doesn't even look good. It makes everyone's head look weirdly shaped. The harsh line where it goes from skin to hair looks unnatural. And within like 4 days it grows out and looks patchy and terrible so you have to go back to the barber every two weeks to maintain it. How is that a good haircut?And don't even get me started on the kids. I see 8 year olds walking around with high skin fades and line ups looking like they're about to drop a soundcloud EP. Let kids look like kids.I genuinely think people only get fades because everyone else has one and they saw it on tiktok or instagram. It's not because it suits their face or their style. It's because the barber asked "the usual?" and they said yes because they have no idea what else to ask for. Sat in the waiting area at my local barbershop yesterday playing jackpot city while six dudes in a row walked out with identical haircuts. We went from having actual variety in men's haircuts to this one single template that 80% of guys copy.It's the men's equivalent of when every girl got the same chunky highlights in 2008 or the same curtain bangs in 2021. Just pure herd mentality."

---

## Data Collection

**Source:** r/changemyview and r/unpopularopinion, public posts only

**Method:** Manual copy-paste into Google Sheets CSV

**Total examples:** 201

**Label distribution:**
| Label | Count |
|---|---|
| Argument | 84 |
| Assertion | 60 |
| Anecdote | 57 |

**3 difficult annotation examples:**

1. Difficult Example 1: A post arguing that fades are ugly because everyone copies the style blindly, with historical comparisons to women's hair trends. Could be Assertion (opinion with no hard data) or Argument (herd mentality framework with specific examples). Decision rule: if examples support a logical chain rather than just restate the claim, label Argument even without external data. Final label: Argument.

2. Difficult Example 2: A post claiming that musicians who cannot read sheet music are objectively worse than those who can, using specific functional benefits like learning songs faster, writing music, and playing in larger ensembles as support. The aggressive dismissive tone made it feel like an Assertion at first, but stripping the tone away revealed a structured logical case underneath. The decision rule applied was that tone does not determine the label, structure does. If reasoning exists that stands independently of the emotional framing, it qualifies as Argument. Final label: Argument.

3. Difficult Example 3: A post from someone working in AI development who shares their personal experience with coworker pushback on automation, while also making broader points about environmental impact, predatory economics, and access controls for AI tools. It felt like a mix of Anecdote and Argument because personal experience and external reasoning were both present. The decision rule applied was the load-bearing test: remove the personal story and does the argument still stand? In this case no, the entire post collapses without the workplace context and personal philosophy driving it. The reasoning exists but it cannot stand on its own. Final label: Anecdote.
---

## Fine-Tuning Approach

**Base model:** distilbert-base-uncased

**Training setup:**
- Epochs: 5
- Learning rate: 5e-5 (changed from default 2e-5)
- Batch size: 8 (changed from default 16)

**Hyperparameter decisions:**

The default settings of 3 epochs, learning rate 2e-5, and batch size 16 produced a 
flatlined validation accuracy of 43% across all epochs, indicating the model was not 
learning. Batch size was reduced from 16 to 8 because with only 140 training examples, 
a batch size of 16 produced only 9 gradient updates per epoch which was insufficient. 
Learning rate was increased from 2e-5 to 5e-5 to allow larger weight updates on this 
small dataset. Epochs were increased from 3 to 5 to give the model more training time. 
Best validation accuracy of 70% was achieved at epoch 4 before slight overfitting at 
epoch 5.
---

## Baseline

**Model:** Groq llama-3.3-70b-versatile, zero-shot

**Prompt approach:** Provided label definitions and instructed the model to output only 
one word. No examples or task-specific training were used.

**Baseline accuracy:** 67.7%

---

## Evaluation Report

### Overall Accuracy

| Model | Accuracy |
|---|---|
| Zero-shot baseline (Groq) | 67.7% |
| Fine-tuned DistilBERT | 64.5% |

Fine-tuning regression: -3.2 points

### Per-Class Metrics

**Baseline (Groq zero-shot):**

| Label | Precision | Recall | F1 | Support |
|---|---|---|---|---|
| Assertion | 0.50 | 0.67 | 0.57 | 9 |
| Anecdote | 1.00 | 0.56 | 0.71 | 9 |
| Argument | 0.71 | 0.77 | 0.74 | 13 |
| Accuracy | | | 0.68 | 31 |

**Fine-tuned DistilBERT:**

| Label | Precision | Recall | F1 | Support |
|---|---|---|---|---|
| Assertion | 0.50 | 0.44 | 0.47 | 9 |
| Anecdote | 0.64 | 0.78 | 0.70 | 9 |
| Argument | 0.75 | 0.69 | 0.72 | 13 |
| Accuracy | | | 0.65 | 31 |

### Confusion Matrix (Fine-tuned Model)

| | Predicted: Assertion | Predicted: Anecdote | Predicted: Argument |
|---|---|---|---|
| True: Assertion | 3 | 1 | 5 |
| True: Anecdote | 2 | 5 | 2 |
| True: Argument | 1 | 0 | 12 |

### 3 Wrong Predictions — Analysis

**Wrong Prediction 1: Ghosting post**
- True label: Assertion
- Predicted: Argument
- The ghosting post uses a claim plus reason structure which on the surface resembles an Argument. The model predicted Argument because of that structure. However the reason provided, "they are still basically a stranger," is itself just another assertion with no external evidence or logical framework behind it. The model learned that claim plus reason equals Argument, but could not evaluate whether the reasoning actually holds up. This reveals a core limitation: DistilBERT detects the presence of reasoning structure but cannot assess its quality or validity. A fourth label distinguishing weak Arguments from strong Arguments may have given DistilBERT a clearer boundary to learn from, allowing it to separate posts that gesture at reasoning from posts that actually demonstrate it.

**Wrong Prediction 2: Obese passenger post**
- True label: Anecdote
- Predicted: Argument
- The obese passenger post opens with a policy claim, that airlines should require obese passengers to book two seats, before revealing the personal story driving it. The model latched onto the policy framing and structural language and predicted Argument. However the entire post collapses without the personal flight experience as its foundation, which is the defining characteristic of an Anecdote under our taxonomy. This was genuinely one of the harder posts to annotate because the policy argument feels substantial on its own. The model failed to correlate the density of first person language, the repeated use of "I," "my," and "me" throughout the post, as a signal that personal experience was load-bearing rather than decorative. A model with more Anecdote training examples that lead with policy claims before revealing personal stories may have learned this pattern more reliably.

**Wrong Prediction 3: Concert recording post**
- True label: Argument
- Predicted: Assertion
- The concert recording post was genuinely difficult to classify even as a human annotator. The opening line "it sucks having all these people watching the show through their phones" uses the kind of casual complaint language that appears frequently in Assertions throughout our dataset. The model likely triggered on that surface pattern and predicted Assertion. However underneath the frustrated tone there is a logical chain: phone recordings degrade the experience for other attendees, people do not actually rewatch their recordings anyway, professional recordings would satisfy the memory need without the disruption, therefore banning phones and providing official recordings solves both problems simultaneously. That reasoning stands independently of any personal story. The overlap between assertive language and actual reasoning is where our three label taxonomy showed its biggest limitation. A weak Argument label would have given the model a middle ground to land on for posts like this one, where the reasoning is present but the tone reads like a complaint, and may have reduced the misclassification of Arguments that do not sound academic or structured on the surface.

### Sample Classifications
| Post (truncated) | True Label | Predicted | Confidence |
|---|---|---|---|
| "If religiously motivated murders were performed by capturing people on a shrine..." | Argument | Argument | 0.93 |
| "Before two people move into a serious commitment, ghosting is a very clear communication..." | Assertion | Argument | 0.48 |
| "Sleepovers should be normal for adults, they're way better than parties..." | Assertion | Assertion | 0.75 |
| "I believe that men need women, and that the harder pairing processes we are seeing..." | Assertion | Argument | 0.93 |
| "I see this as a baseless conspiracy that has gone weirdly mainstream..." | Assertion | Argument | 0.78 |

The religious murders post was correctly predicted as Argument with high confidence (0.93) because it contains a clear logical chain connecting location, intent, and religious classification across multiple structured steps, exactly the kind of reasoning pattern the model learned to associate with the Argument label.

---

## Reflection: What the Model Learned vs What I Intended

What the Model Learned vs What I Intended
What I intended DistilBERT to learn was the structural distinction between three types of posts: ones that make bare claims, ones driven by personal experience, and ones built on logical reasoning or evidence. What it actually learned was surface level language patterns. Argument posts on Reddit tend to use structured confident language, numbered points, and references to external concepts, so the model learned to associate that vocabulary with the Argument label. Assertion posts tend to be shorter and more emotionally direct, so the model learned that pattern too. The boundary it never fully learned was the one that mattered most: the difference between a claim that gestures at reasoning and a claim that actually demonstrates it. As the model trained across more epochs it improved, but simultaneously began overfitting to specific word patterns in the training data rather than the underlying structural distinction the labels were designed to capture. With a larger dataset and a possible fourth label separating weak Arguments from strong ones, the model may have learned something closer to what was intended.

---

## Spec Reflection

**One way the spec helped:** The requirement to collect data manually kept me close to 
the text in a way that genuinely improved annotation quality. Reading each post 
individually forced me to develop consistent decision rules for edge cases that would 
have been impossible to anticipate before seeing real examples.

**One way implementation diverged:** The spec suggested using default hyperparameters 
as a starting point, but the default settings produced a flatlined validation accuracy 
of 43% across all epochs indicating the model was not learning at all. Batch size was 
reduced from 16 to 8, learning rate increased from 2e-5 to 5e-5, and epochs increased 
from 3 to 5. These changes improved accuracy from 43% to a peak validation accuracy of 
70% at epoch 4, which was a necessary divergence given the small dataset size.

---

## AI Usage

**Instance 1:**
During the manual annotation process I directed Claude to review posts I was uncertain about and confirm or challenge my label decision. For each uncertain post I provided my suspected label and reasoning, and Claude would either confirm it or push back with a counter argument explaining which label better fit the structural definition. This was not pre-labeling. Every final label decision was mine. Claude served as a sounding board that helped me apply my decision rules consistently across 201 examples, particularly on edge cases where Assertion and weak Argument overlapped. Several label decisions were overridden after Claude's pushback, including the service worker post and the morality post early in annotation.

**Instance 2:**
When the default training settings produced a flatlined validation accuracy of 43% across all three epochs I directed Claude to explain what each hyperparameter controlled and how to adjust them for a small dataset. Claude explained that batch size 16 was producing too few gradient updates per epoch for 140 training examples, that learning rate 2e-5 was too conservative for this dataset size, and that more epochs were needed since the model was still improving at epoch 3. I applied those changes incrementally, testing batch size first, then learning rate, then epochs, and documented each change and its effect on validation accuracy in the README

**Annotation assistance:**
Claude was not used to pre-label any examples in bulk. All 201 labels were assigned by me during manual review. Claude was consulted on individual uncertain posts during the annotation process as described in Instance 1 above.

## Demo Video

[Watch the demo here](https://www.loom.com/share/b6e635bd94944c60a37cba43cc4c84c2)
