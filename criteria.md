# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. Overall Accuracy $\ge 0.65$

<!-- Your criterion. It must name a number. -->



**Why this target:** Since a dummy model guessing only the majority class (feature_evaluation) gets 51.5% by default, hitting 65% accuracy proves the model is picking up meaningful signals across categories without setting an unrealistic bar for a small 200-review dataset.



---

## 2. Minority Class (low_effort) Macro F1 => 0.50

<!-- Your criterion. -->



**Why this target:** With only 39 examples of low_effort (~19.5% of the data), the model doesn't have many patterns to learn from. A target F1 of 0.50 keeps the expectation reasonable while ensuring the model doesn't completely fail at identifying low-substance reviews.



---

## 3. Per-label minimum F1 >= 0.6 for Core Classes

<!-- Your criterion. -->



**Why this target:** Because feature_evaluation (103 reviews) and personal_story (58 reviews) often overlap when users tell stories with slight hardware details, boundary confusion will happen. Aiming for an F1 of 0.60 across both core categories gives the model room for error while still proving it can separate subjective narratives from hard technical facts.



---

## 4. Inter-Annotator Consistency (Cohen's Kappa >= 0.60) 

<!-- Your criterion. -->



**Why this target:**Subjective edge cases (like distinguishing between subjective noise complaints and concrete specs) naturally cause disagreement. A Kappa score of 0.60 reflects moderate-to-substantial agreement, showing my boundary rules are clear enough to be reliable without requiring perfect human consensus.



---

## 5. Confidence >= 0.70

<!-- Your criterion. -->



**Why this target:** When the model is reasonably confident, it should be right at least 70% of the time. Lowering this threshold accounts for model uncertainty on nuanced text while still giving me a usable slice of automated predictions I can trust.



---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
