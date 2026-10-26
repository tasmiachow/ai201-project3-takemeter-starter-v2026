# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->

This project analyzes e-commerce product reviews, specifically on Amazon, within the Tech and Furniture sectors to cut through online noise and surface genuine hardware insights. The classifier sorts incoming reviews into a rigorous three-tier framework: feature_evaluation for concrete technical parameters and structural tolerances, personal_story for lifestyle and setup narratives, and low_effort for shipping logistics and uninformative praise. By automating this pipeline, buyers and builders can instantly isolate actionable hardware intelligence without wading through generic sentiment or box-weight complaints.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### feature_evaluation

**Definition:** The review cites specific, verifiable technical parameters, structural tolerances, material properties, unadvertised physical constraints, or benchmark-backed performance.

**Example 1:** Super high quality look, it immediately elevated my apartment aesthetic. It was super easy to assemble all I used was an electric drill and a hammer (the hammer was only used once for the first part of the instructions) . Overall I built it in one hour and 20 mins. The instructions are super straightforward. 10/10... It fits 14 pairs of my shoes and I’m a size 7 1/2.
>

**Example 2:**FINALLY figured out how to optimize a GPU, CPU, RAM, and now my gaming PC is bordering on professional gaming settings. Although it has overclocking capabilities, I haven’t even overclocked this bad boy. I read many reviews that said Gigabyte GPUs are extremely loud, but generally speaking, that’s not the case here. I rarely hear my GPU revving up to the point that it distracts from what I’m listening to. Everything about this GPU screams stability, including performance and thermals. The only issues I’ve had were because of a learning-curve. My first ever PC build and I’m very happy! Although, my wallet doesn’t feel that way. GPUs are not very budget-friendly.

Warzone Specs:

FPS: 350+ (average)
FPS: 500ish (peak)
FPS: 75ish (1% lows)
I’ve limited to FPS to 240.
Latency: 14 (peak)
Latency: 4 (average)
Temperature: 35ish (idle)
Temperature: 75ish (under stress)
Usage: 0% (idle)
Usage: 95ish (under stress)

The Adrenaline App makes for extreme customization. AMD won me over for sure! #TeamRed!
2 people found this helpful
>

### personal_story

**Definition:** The review centers on subjective user narratives, lifestyle context, personal setup baselines, qualitative impressions, or comparative statements based on individual preference rather than objective testing.

**Example 1:** A very beautiful piece, adds to your home decor instead of taking away from it with the normal tacky shoe racks. If you have small children it will definitely hold double the shoes!
>

**Example 2:** This shoe cabinet looks magnificent in our small farm house. The shoes lying by the front door were driving me insane so it’s nice to have somewhere to put them now in order to save floor space. This cabinet was a breeze to build since the instructions were easy to follow. I will say that I messed up in the beginning and let the cabinet and so the bottom back support did crack the wood where the screws were since it’s thin, but that’s user error and not a manufacture error. Just know to be gentle while constructing this cabinet. It looks incredible and holds large shoe sizes which is great compared to some other ones I looked at. Terrific value for such a visually high-end product and it really adds character to our living room!!
>


### low_effort

**Definition:** The review contains non-substantive or generic sentiment, relies on single-line transactional mentions, echoes advertised baseline features without evaluation, or focuses entirely on unboxing or courier shipping logistics.

**Example 1:**: Looks really nice!

**Example 2:** Looks really nice!

### The hardest boundary

**Which two labels:** feature_evaluation vs. personal_story

**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->

If a post details specific physical hardware behavior, structural component limits, or unadvertised mechanical defects during setup or use—even if framed within a personal build narrative—it is classified as feature_evaluation; if it relies solely on qualitative adjectives or personal frustration without naming concrete structural parameters, it is classified as personal_story.

---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:** Amazon Reviews

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. --> I labeled them all myself. However I did ask AI to weigh in on some reviews, now looking back that was probably why the accuracy was so low.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| feature_evaluation | 102| 51% |
| personal_story | 59 | 29.5% |
| low_effort | 39 | 19.5% |
| **Total** | 200 | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:* I really love this keyboard it’s really cute and I like how the keys sound- just a little bit of click but not too loud. I noticed some bad reviews about the mouse but honestly I don’t mind the mouse
>
> *Could have been:* feature_evaluation or personal_story
>
> *I chose, because:*I chose personal_story, because: Even though it mentions tactile attributes (key sound and mouse feel), it leans entirely on subjective lifestyle impressions and personal reassurance rather than testing concrete performance tolerances or technical parameters.

**2.**
> *The post:* The metal is very thin and once put together will work as indicated. It is very easily bent. The packaging was great and well cushioned. The doors were a little crooked and the magnets could perhaps be a little more powerful to hold closed. Other than that they are aesthetically well designed.
>
> *Could have been:* feature_evaluation or personal_story
>
> *I chose, because:* I chose feature_evaluation, because: It details specific physical structural properties, material thickness, and component alignment flaws (feature_evaluation) rather than just offering a passing, uninformative shipping comment.

**3.**
> *The post:* As a mom of 3 who works from home, my phone is constantly in use between work calls, emails, appointments, and keeping up with my kids. This power bank has been a lifesaver. I love that it magnetically attaches to my phone and charges without me having to search for a cable.The battery lasts a long time, and the built-in cables make it super convenient when I need to charge other devices too. It's easy to throw in my bag when we're running errands or heading to activities.Overall, it's reliable, easy to use, and gives me peace of mind knowing my phone won't die in the middle of a busy day.
>
> *Could have been:* feature_evaluation or personal_story
>
> *I chose, because:*I chose personal_story, because: It focuses heavily on lifestyle context, personal daily routines, and family utility narrative (personal_story) rather than citing verifiable charging speeds, battery capacity metrics, or voltage specs.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:** distilbert-base-uncased

**Settings:** <!-- epochs, learning rate, batch size, seed --> 
EPOCHS = 3
LEARNING_RATE = 2e-5
BATCH_SIZE = 16

**Anything I changed from the defaults, and why:** N/A. Did not change anything.

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. --> label                               
feature_evaluation     71   16    15
personal_story         41    9     9
low_effort             27    6     6

[note] 'low_effort' has only 6 examples in the test split.

A metric computed on that few examples moves a lot between seeds.



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* Assistance in writing a Python script to take my raw amazon_reviews with many extra columns and convert it to the labels.csv file matched the expected column structure .
- *What came back:* It truncated the extra rows and filters on my original spreadsheet to match the required rows (post, label, notes)
- *What I changed:* Ran the script and verified that notes still carried the review title and product category 

**Moment 2**

- *What I asked for:* An analysis of the scraped review dataset to check for class balance and identify any exact text duplicates.
- *What came back:* A distribution count showing 200 total posts along with the discovery of 4 exact duplicate review pairs across the dataset.
- *What I changed:* Dropped the 4 duplicate records down to 196 unique posts to completely prevent data leakage from landing identical samples across different splits.

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
